<template>
  <div class="form-item-split">
    <div class="form-item-area"></div>
  </div>
</template>

<script>
export default {
  data () {
    return {
    }
  }
}
</script>

<style scoped lang="less">
.form-item-split{
  border: solid 3px red;
  border-top: solid 3px rgba(0,0,0,0);
  border-bottom: solid 3px rgba(0,0,0,0);
  .form-item-area{
    height: 3px;
    background-color: red;
  }
}
</style>
