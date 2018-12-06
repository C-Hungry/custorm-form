<template>
  <div class="form-item-datetime-local">
    <div class="form-item-row">
      <div class="form-item-arrow">
        <div class="form-item-top"></div>
        <div class="form-item-bottom"></div>
      </div>
      <form-item-field :name="'开始时间'">
        <input type="text" :placeholder="'请选择'" :value="field.value.split(',')[0]" readonly>
        <input type="datetime-local" v-model="valueStart" @change="changeStart()" :readonly="field.readonly">
      </form-item-field>
    </div>
    <div class="form-item-row">
      <div class="form-item-arrow">
        <div class="form-item-top"></div>
        <div class="form-item-bottom"></div>
      </div>
      <form-item-field :name="'结束日期'">
        <input type="text" :placeholder="'请选择'" :value="field.value.split(',')[1]" readonly>
        <input type="datetime-local" v-model="valueEnd" @change="changeEnd()" :readonly="field.readonly">
      </form-item-field>
    </div>
  </div>
</template>

<script>
import formItemField from "./form-item.vue"
export default {
  components:{
    formItemField
  },
  data () {
    return {
      valueStart: "",
      valueEnd: ""
    }
  },
  methods:{
    changeStart(){
      var arr = this.field.value.split(',');
      arr[0] = this.valueStart;
      this.field.value = arr.join(',');
      console.log(this.field.value)
    },
    changeEnd(){
      var arr = this.field.value.split(',');
      arr[1] = this.valueEnd;
      this.field.value = arr.join(',');
      console.log(this.field.value)
    },
  },
  compute:{
    value(){
      return this.field.value;
    },
  },
  watch:{
    value(){
      var arr = this.field.value.split(',');
      this.valueStart = arr[0];
      this.valueEnd = arr[1];
      this.field.displayValue = this.field.value;
    },
  },
  props:{
    field: {
      type: Object,
      default: null
    }
  },
}
</script>

<style scoped lang="less">
.form-item-datetime-local{
  .form-item-row{
    position: relative;
    input[type=datetime-local]{
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      opacity: 0;
    }
    .form-item-arrow{
      position: absolute;
      right: 5px;
      top: 50%;
      transform: translate(0,-50%);
      width: 6px;
      height: 12px;
      .form-item-top{
        width: 6px;
        height: 6px;
        background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%"><line x1="0" y1="0" x2="100%" y2="100%" stroke="%23ccc" stroke-width="1"/></svg>');
      }
      .form-item-bottom{
        width: 6px;
        height: 6px;
        background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%"><line x1="100%" y1="0" x2="0%" y2="100%" stroke="%23ccc" stroke-width="1"/></svg>');
      }
    }
  }
  .form-item-row:first-child{
    border-bottom: solid 1px rgba(0, 0, 0, 0.1);
  }
}
</style>
