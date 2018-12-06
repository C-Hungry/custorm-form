<template>
  <div class="form-detail">
    <div v-if="current.field">
      <div class="form-detail-item">
        <div class="form-detail-title">
          字段：
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="current.field.name">
        </div>
      </div>
      <div class="form-detail-item">
        <div class="form-detail-title">
          提示：
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="current.field.placeholder">
        </div>
      </div>
      <div v-if="current.field.type=='text'||current.field.type=='number'" class="form-detail-item">
        <div class="form-detail-title">
          验证：
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="current.field.regex">
        </div>
      </div>
      <div v-if="current.field.type=='textarea'" class="form-detail-item">
        <div class="form-detail-title">
          最大长度：
        </div>
        <div class="form-detail-value">
          <input type="number" v-model="current.field.maxLen">
        </div>
      </div>
      <div class="form-detail-item">
        <div class="form-detail-title">
          必填：
        </div>
        <div class="form-detail-value">
          <input type="checkbox" v-model="current.field.require">
        </div>
      </div>
      <div class="form-detail-item">
        <div class="form-detail-title">
          列表展示：
        </div>
        <div class="form-detail-value">
          <input type="checkbox" v-model="current.field.showInProfile">
        </div>
      </div>
      <div v-if="current.field.type=='multiselect'||current.field.type=='select'" class="form-detail-item">
        <div class="form-detail-title">
          列表：
        </div>
        <div class="form-detail-value">
          <a @click="switchSource()" style="cursor: pointer; color: rgba(192,192,255,0.7);">切换来源</a>
          <a v-if="current.field.datasource.from=='list'" @click="newItem()" style="cursor: pointer; color: rgba(192,192,255,0.7);">新增项</a>
        </div>
      </div>
      <div v-if="current.field.datasource.from=='list'&&(current.field.type=='multiselect'||current.field.type=='select')" v-for="(item,index) in current.field.datasource.list" class="form-detail-item">
        <div class="form-detail-title">
          <input type="text" v-model="item.value" placeholder="选项值" style="width: 40%; max-width: 43px; text-align: center;">
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="item.name" placeholder="显示文本" style="position: relative; top: 1px;">
          <a @click="deleteItem(item)" style="cursor: pointer;">X</a>
        </div>
      </div>
      <div v-if="current.field.datasource.from=='src'&&(current.field.type=='multiselect'||current.field.type=='select')" class="form-detail-item">
        <div class="form-detail-title">
          地址：
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="current.field.datasource.src" placeholder="">
        </div>
      </div>
      <div v-if="current.field.datasource.from=='src'&&(current.field.type=='multiselect'||current.field.type=='select')" class="form-detail-item">
        <div class="form-detail-title">
          方法：
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="current.field.datasource.methods" placeholder="">
        </div>
      </div>
      <div v-if="current.field.type=='text'" class="form-detail-item">
        <div class="form-detail-title">
          地址：
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="current.field.datasource.src" placeholder="">
        </div>
      </div>
      <div v-if="current.field.type=='text'" class="form-detail-item">
        <div class="form-detail-title">
          方法：
        </div>
        <div class="form-detail-value">
          <input type="text" v-model="current.field.datasource.methods" placeholder="">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "form-detail",
  data () {
    return {};
  },
  methods:{
    switchSource(){
      this.current.field.datasource.from = this.current.field.datasource.from == "list" ? "src" : "list";
    },
    newItem(){
      this.current.field.datasource.list.push({
        value: this.current.field.datasource.list.length + 1,
        name: "选项" + (this.current.field.datasource.list.length + 1),
      });
    },
    deleteItem(item){
      var index = this.current.field.datasource.list.indexOf(item);
      if(index>=0) this.current.field.datasource.list.splice(index,1);
    }
  },
  props:{
    current:{
      type: Object,
      default: ()=>{return {
        field: null
      }},
    },
  }
}
</script>

<style scoped lang="less">
.form-detail{
  line-height: 40px;
  color: rgba(255, 255, 255, 0.6);
  .form-detail-item{
    display: flex;
    .form-detail-title{
      flex: 1;
      text-align: right;
    }
    .form-detail-value{
      flex: 2;
    }
    input[type=text],input[type=number]{
      display: inline-block;
      margin-left: 4px;
      padding: 2px;
      width: 80%;
      border: solid 1px rgba(0, 0, 0, 0.1);
      background-color: rgba(0, 0, 0, 0);
      color: rgba(255, 255, 255, 0.6);
      outline: none;
    }
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
      -webkit-appearance: none;
    }
    input[type="number"] {
      -moz-appearance: textfield;
    }
  }
}
</style>
