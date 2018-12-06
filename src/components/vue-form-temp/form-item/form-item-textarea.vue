<template>
  <div class="form-item-textarea">
    <form-item-field :name="field.name" :height="80">
      <textarea v-model="field.value" :placeholder="field.placeholder" :maxlength="field.maxLen" :readonly="field.readonly" style="height: 60px;">
      </textarea>
    </form-item-field>
  </div>
</template>

<script>
import formItemField from "./form-itemH.vue"
export default {
  components:{
    formItemField
  },
  data () {
    return {}
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
