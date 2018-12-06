<template>
  <div class="form-item-number">
    <form-item-field :name="field.name">
      <input type="number" v-model="field.value" :placeholder="field.placeholder" :readonly="field.readonly">
    </form-item-field>
  </div>
</template>

<script>
  import formItemField from "./form-item.vue"
  export default {
    components: {
      formItemField
    },
    data() {
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
    props: {
      field: {
        type: Object,
        default: null
      }
    },
  }
</script>

<style scoped lang="less">
  .form-item-number {
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
      -webkit-appearance: none;
    }
    input[type="number"] {
      -moz-appearance: textfield;
    }
  }
</style>
