<template>
  <div class="form-item-single">
    <div class="form-item-arrow">
      <div class="form-item-top"></div>
      <div class="form-item-bottom"></div>
    </div>
    <form-item-field :name="field.name">
      <input type="text" :placeholder="field.placeholder" :value="field.displayValue" readonly>
      <select v-model="field.value" :disabled="field.readonly">
        <option v-for="item in field.datasource.list" :value="item.value">{{item.name}}</option>
      </select>
    </form-item-field>
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
    }
  },
  watch:{
    value(){
      this.field.displayValue = this.getCurrentName();
    },
  },
  computed:{
    value(){
      return this.field.value;
    },
  },
  methods:{
    getCurrentName(){
      if(!this.field.value) return "";
      var arr = this.field.datasource.list.filter(x=>x.value==this.field.value);
      return arr.length > 0 ? arr[0].name : "未知";
    }
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
.form-item-single{
  select{
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
</style>
