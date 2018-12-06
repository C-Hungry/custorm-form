<template>
  <div class="form-item-mult">
    <div class="form-item-arrow">
      <div class="form-item-top"></div>
      <div class="form-item-bottom"></div>
    </div>
    <form-item-field :name="field.name">
      <input type="text" :placeholder="field.placeholder" :value="getCheckedName()" readonly @click="show=true">
      <div v-if="show" class="form-item-layer" @click="show=false">
        <div class="form-item-list" @click="$event.cancelBubble=true">
          <div v-for="(item,index) in field.datasource.list" class="form-item-item">
            <input type="checkbox" :id="unique+'-'+index" v-model="item.checked">
            <label :for="unique+'-'+index" style="padding-left: 5px;">{{item.name}}</label>
          </div>
        </div>
      </div>
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
      show: false,
      unique: "multiselect" + Math.random() * 100000
    }
  },
  watch:{
    value(){
      this.field.displayValue = this.getCheckedName();
    },
  },
  computed:{
    value(){
      return this.field.value;
    },
  },
  methods:{
    getCheckedName(){
      return this.field.datasource.list.filter(x=>x.checked).map(x=>x.name).join(",");
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
.form-item-mult{
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
  .form-item-layer{
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0,0,0,0.4);
    overflow-y: auto;
    z-index: 9;
    .form-item-close{
      width: 30px;
      height: 30px;
      border-radius: 15px;
      background-color: rgba(0,0,0,0.3);
      color: rgba(255,255,255,0.8);
      position: absolute;
      top: 10px;
      right: 10px;
      text-align: center;
      line-height: 30px;
    }
    .form-item-list{
      position: absolute;
      top: 50%;
      left: 10px;
      right: 10px;
      transform: translate(0,-50%);
      padding: 10px;
      background-color: rgba(255,255,255,1);
      .form-item-item{
        line-height: 40px;
        padding: 0 5px;
        font-weight: bold;
        input[type=checkbox]{
          width: 20px;
          height: 20px;
          position: relative;
          top: 5px;
        }
      }
    }
  }
}
</style>
