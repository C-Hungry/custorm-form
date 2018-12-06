<style scoped lang="less">
  .print-designer {
    display: flex;
    flex-direction: row;
    .print-item-box{
      flex: 1;
      line-height: 30px;
      .print-item{
        margin-top: 5px;
        text-align: center;
        cursor: pointer;
        display: block;
        color: rgba(255, 255, 255, 0.6);
        border: solid 1px rgba(255, 255, 255, 0.6);
      }
      .print-item:first-child{
        margin-top: 0;
      }
    }
  }
</style>

<template>
  <div class="print-designer">
    <iframe ref="designer" width="100%" height="100%" frameborder="0" style="flex: 3; padding: 5px; background-color: white; margin: 0 5px 0 0; height: 100%;"></iframe>
    <div class="print-item-box" onselectstart="return false;">
      <div v-if="isBaseTemp" v-for="row in rows" class="print-item" v-on:click="command(row,$event)">{{row.name}}</div>
      <div class="print-item" v-on:click="init(row,$event)">
        清空模板
      </div>
      <div class="print-item" v-on:click="print(row,$event)">
        打印预览
      </div>
      <div class="print-item" style="position: relative;">
        导入
        <input type="file" ref="importFile" v-on:click="clearImportFile" v-on:change="importFileChanged" style="position: absolute; top: 0; left: 0; bottom: 0; right: 0; opacity: 0; cursor: pointer;">
      </div>
      <template>
        <div ref="print-title" style="display: none;">
          <div class="print-title" contenteditable="true">
            XXXXXX打印模板
          </div>
        </div>
        <div ref="print-no" style="display: none;">
          <div class="print-no" contenteditable="true">
            编号：YX201807010001
          </div>
        </div>
        <div ref="print-line" style="display: none;">
          <div class="print-row print-row0"></div>
        </div>
        <div ref="print-col4" style="display: none;">
          <div class="print-row print-row2">
            <div contenteditable="true">
                姓名
            </div>
            <div contenteditable="true">
                张三
            </div>
            <div contenteditable="true">
                部门
            </div>
            <div contenteditable="true" style="border-right: 0;">
                研发部
            </div>
          </div>
        </div>
        <div ref="print-col2" style="display: none;">
          <div class="print-row print-row1">
            <div class="title" contenteditable="true">
                备注
            </div>
            <div class="print-value">
              <div contenteditable="true">
                测试备注
              </div>
            </div>
          </div>
        </div>
        <div ref="print-col2-h" style="display: none;">
          <div class="print-row print-row1-h">
            <div class="title" contenteditable="true">
                申请人
            </div>
            <div class="print-value">
              <div contenteditable="true">
                同意<br>
                李四<br>
                2018-01-01 18:30
              </div>
            </div>
          </div>
        </div>
        <div ref="print-foot" style="display: none;">
          <div class="print-foot" contenteditable="true">
            1.该审批单一式三份，由燃料部、策划部、燃供部存留<br/>
            2.车辆验票异常时申请审批单
          </div>
        </div>
        <div ref="print-pagebreak" style="display: none;">
          <div class="page-break">
            <div class="no-print"><hr/><span>分页</span><hr/></div>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
  export default {
    name: "print-designer",
    data() {
      return {
        style: `
          <!-- 基础模板 -->
          <style>
            @media print{
              @page {
                size: portrait;
                margin: 30px;
              }
              .page-break{
                page-break-after: always;
              }
              .no-print{
                display: none;
              }
              .no-print>*{
                display: none;
              }
            }   
            body::-webkit-scrollbar
            {
                width: 0px;
                height: 0px;
            }
            body::-webkit-scrollbar-track-piece
            {
                background-color: rgba(255, 255, 255, 0.1);
                -webkit-border-radius: 0px;
            }
            body::-webkit-scrollbar-thumb:vertical
            {
                width: 0px;
                background-color: rgba(255, 255, 255, 0.4);
                -webkit-border-radius: 0px;
            }
            body{
              margin: 0;
              padding: 0;
              font-family: Microsoft YaHei;
              font-size: 14px;
              color: #333;
              min-height: 400px;
              width: 100%;
              background-color: #fff;
              overflow-y: auto;
            }
            body *{
              outline: none;
            }
            .print-title{
              padding-top: 10px;
              height: 50px;
              line-height: 50px;
              width: 99.5%;
              font-size: 20px;
              font-weight: bold;
              text-align: center;
              display: table;
              position: relative;
            }
            .print-no{
              height: 30px;
              line-height: 30px;
              width: 99.5%;
              font-size: 14px;
              font-weight: normal;
              text-align: right;
              display: table;
              position: relative;
            }
            .print-row{
              width: 99.5%;
              font-size: 14px;
              font-weight: normal;
              text-align: right;
              border: solid 1px #333;
              border-top: 0;
              text-align: center;
              position: relative;
            }
            .print-row0{
              height: 0;
              border-bottom: solid 1px #333;
            }
            .print-row1{
              min-height: 50px;
              line-height: 50px;
              display: flex;
            }
            .print-row1>.title{
              flex: 1;
              border-right: solid 1px #333;
            }
            .print-row1>.print-value{
              flex: 3;
              padding-right: 2px;
            }
            .print-row1>.print-value>div{
              text-align: left;
              padding: 10px;
              line-height: 30px;
            }
            .print-row1-h{
              min-height: 120px;
              line-height: 120px;
              display: flex;
            }
            .print-row1-h>.title{
              flex: 1;
              border-right: solid 1px #333;
            }
            .print-row1-h>.print-value{
              flex: 3;
              padding-right: 2px;
            }
            .print-row1-h>.print-value>div{
              text-align: left;
              padding: 15px 10px;
              line-height: 30px;
            }
            .print-row2{
              height: 50px;
              line-height: 50px;
              display: flex;
            }
            .print-row2>div{
              flex: 1;
              border-right: solid 1px #333;
            }
            .print-foot{
              min-height: 50px;
              width: 99.5%;
              position: relative;
            }
            .page-break{
              min-height: 50px;
              position: relative;
            }
            .no-print{
              text-align: center;
              display: flex;
              height: 50px;
              line-height: 50px;
            }
            .no-print>hr{
              margin-top: 24px;
              height: 0px;
            }
            .no-print>*{
              flex: 1;
            }
          </style>
        `,
        rows:[
          {
            name: "插入模板标题",
            ref: "print-title",
          },
          {
            name: "插入模板编号",
            ref: "print-no",
          },
          {
            name: "插入起始线段",
            ref: "print-line",
          },
          {
            name: "插入1×4",
            ref: "print-col4",
          },
          {
            name: "插入1×2-1",
            ref: "print-col2",
          },
          {
            name: "插入1×2-2",
            ref: "print-col2-h",
          },
          {
            name: "插入模板页脚",
            ref: "print-foot",
          },
          {
            name: "插入分页",
            ref: "print-pagebreak",
          },
          {
            name: "删除当前行",
            action: ()=>{
              console.log(this.currentIndex)
              if(this.currentIndex==-1){
                alert("未选择任何行！");
                return;
              }
              var item = this.$refs.designer.contentWindow.document.body.children[this.currentIndex];
              this.$refs.designer.contentWindow.document.body.removeChild(item);
              this.currentIndex = -1;
            }
          },
        ],

        currentIndex: -1,

        isBaseTemp: false,
      };
    },
    methods:{
      getIsBaseTemp(){
        this.isBaseTemp = this.$refs.designer.contentWindow.document.body.innerHTML.indexOf("<!-- 基础模板 -->") >= 0;
      },
      load(tempStr){
        this.$refs.designer.contentWindow.document.body.innerHTML = tempStr;
        this.bindClickEvent();
        this.getIsBaseTemp();
      },
      getTempStr(){
        return this.$refs.designer.contentWindow.document.body.innerHTML.replace(/ +/g, " ");
      },
      init(){
        this.$refs.designer.contentWindow.document.body.innerHTML = this.style;
        this.currentIndex = -1;
        this.getIsBaseTemp();
      },
      print(){
        this.$refs.designer.contentWindow.print();
      },
      clearImportFile(){
        this.$refs.importFile.value = "";
      },
      importFileChanged(event){
        var reader = new FileReader();
        reader.readAsText(this.$refs.importFile.files[0]);
				reader.onload = ()=>{
          this.$refs.designer.contentWindow.document.body.innerHTML = reader.result;
          this.getIsBaseTemp();
        }
      },
      command(row){
        var doc = this.$refs.designer.contentWindow.document;
        if(row.action){
          row.action();
        }
        else{
          if(this.currentIndex!=-1){
            doc.body.children[this.currentIndex].after(new this.$refs.designer.contentWindow.DOMParser().parseFromString(this.$refs[row.ref].innerHTML,"text/html").children[0]);
          }
          else{
            doc.body.appendChild(new this.$refs.designer.contentWindow.DOMParser().parseFromString(this.$refs[row.ref].innerHTML,"text/html").children[0]);
          }
          doc.body.innerHTML += "";
        }
        this.bindClickEvent();
        this.getIsBaseTemp();
      },
      bindClickEvent(){
        var doc = this.$refs.designer.contentWindow.document;
        var self = this;
        for(let i = 0; i < doc.body.children.length; i++){
          var item = doc.body.children[i];
          item.onclick = function(){
            self.currentIndex = i;
          }
        }
      }
    },
    mounted(){
      this.init();
    }
  }
</script>
