<template>
  <div class="form-item-text">
    <form-item-field :name="field.name">
      <input type="text" v-model="field.value" :readonly="field.readonly" :placeholder="field.placeholder">
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
      this.field.displayValue = this.value;
    },
  },
  computed:{
    value(){
      return this.field.value;
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
</style>
