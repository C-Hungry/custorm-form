<template>
  <div class="form-item-textnote">
    {{field.placeholder?field.placeholder:'说明'}}
  </div>
</template>

<script>
export default {
  data () {
    return {
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
.form-item-textnote{
  line-height: 30px;
  padding-left: 10px;
  font-size: 14px;
  color: rgba(0,0,0,0.7);
}
</style>
