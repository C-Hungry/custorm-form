<template>
  <div class="form-item-box" onselectstart="return false;">
    <div v-for="field in fields" class="form-item-box-item" draggable="true"
      v-on:dragstart="onDragStart(field,$event)">{{field.name}}</div>
  </div>
</template>

<script>
export default {
  name: "form-item-box",
  data () {
    return {
      fields:[
        {
          drop: "",
          type: "text",
          name: "文本",
          value: "",
          placeholder: "请输入",
          require: false,
          datasource: {
            from: "list",
            list: [],
            src: "",
            methods: "",
          },
          maxLen: 0,
          regex: "",
          showInProfile: false,
        },
        {
          drop: "",
          type: "textarea",
          name: "多行文本",
          value: "",
          placeholder: "请输入",
          require: false,
          datasource: {
            from: "list",
            list: [],
            src: "",
            methods: "GET",
          },
          maxLen: 20,
          regex: "",
          showInProfile: false,
        },
        {
          drop: "",
          type: "number",
          name: "数字",
          value: "",
          placeholder: "请输入",
          require: false,
          datasource: {
            from: "list",
            list: [],
            src: "",
            methods: "GET",
          },
          maxLen: 0,
          regex: "",
          showInProfile: false,
        },
        {
          drop: "",
          type: "select",
          name: "单选",
          value: "",
          placeholder: "请选择",
          require: false,
          datasource: {
            from: "list",
            list: [],
            src: "",
            methods: "GET",
          },
          maxLen: 0,
          regex: "",
          showInProfile: false,
        },
        {
          drop: "",
          type: "multiselect",
          name: "多选",
          value: "",
          placeholder: "请选择",
          require: false,
          datasource: {
            from: "list",
            list: [],
            src: "",
            methods: "GET",
          },
          maxLen: 0,
          regex: "",
          showInProfile: false,
        },
        {
          drop: "",
          type: "date",
          name: "日期",
          value: "",
          placeholder: "请选择",
          require: false,
          datasource: {
            from: "list",
            list: [],
            src: "",
            methods: "GET",
          },
          maxLen: 0,
          regex: "",
          showInProfile: false,
        },
        {
          drop: "",
          type: "datetime",
          name: "日期时间",
          value: "",
          placeholder: "请选择",
          require: false,
          datasource: {
            from: "list",
            list: [],
            src: "",
            methods: "GET",
          },
          maxLen: 0,
          regex: "",
          showInProfile: false,
        },
        // {
        //   drop: "",
        //   type: "daterange",
        //   name: "日期区间",
        //   value: "",
        //   placeholder: "请选择",
        //   require: false,
        //   datasource: {
        //     from: "list",
        //     list: [],
        //     src: "",
        //     methods: "GET",
        //   },
        //   maxLen: 0,
        //   regex: ""
        // },
        // {
        //   drop: "",
        //   type: "datetimerange",
        //   name: "时间区间",
        //   value: "",
        //   placeholder: "请选择",
        //   require: false,
        //   datasource: {
        //     from: "list",
        //     list: [],
        //     src: "",
        //     methods: "GET",
        //   },
        //   maxLen: 0,
        //   regex: ""
        // },
        // {
        //   drop: "",
        //   type: "photo",
        //   name: "图片",
        //   value: "",
        //   placeholder: "请选择",
        //   require: false,
        //   datasource: {
        //     from: "list",
        //     list: [],
        //     src: "",
        //     methods: "GET",
        //   },
        //   maxLen: 0,
        //   regex: ""
        // },
        // {
        //   drop: "",
        //   type: "textnote",
        //   name: "说明",
        //   value: "",
        //   placeholder: "说明",
        //   require: false,
        //   datasource: {
        //     from: "list",
        //     list: [],
        //     src: "",
        //     methods: "GET",
        //   },
        //   maxLen: 0,
        //   regex: ""
        // },
      ]
    }
  },
  methods:{
    onDragStart(field, event){
      window.__dragInHandField = JSON.parse(JSON.stringify(field));
    },
  }
}
</script>

<style scoped lang="less">
.form-item-box{
  line-height: 30px;
  .form-item-box-item{
    margin-top: 5px;
    text-align: center;
    cursor: move;
    display: inline-block;
    width: 100%;
    max-width: 100px;
    color: rgba(255, 255, 255, 0.6);
    border: dashed 1px rgba(255, 255, 255, 0.6);
  }
}
</style>
