<template>
  <div class="form-item-field">
    <div class="form-item-title">{{name}}：</div>
    <div class="form-item-value">
      <slot name="default"></slot>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
    }
  },
  props:{
    name: {
      type: String,
      default: ""
    }
  },
}
</script>

<style scoped lang="less">
.form-item-field{
  height: 40px;
  line-height: 40px;
  display: flex;
  flex-direction: row;
  font-size: 14px;
  .form-item-title{
    flex: 1;
    padding: 0 10px;
    color: rgba(0,0,0,0.7);
  }
  .form-item-value{
    flex: 2;
    position: relative;
    line-height: 20px;
    display: flex;
    input[type=text],input[type=number],input[type=date],input[type=time],input[type=datetime-local],input[type=file],select,textarea{
      border: none;
      outline: none;
      margin: 10px 0;
      padding: 0 15px 0 0;
      height: 20px;
      width: 100%;
      background-color: rgba(0,0,0,0);
      color: #666;
      text-align: right;
    }
    select{
      opacity: 0;
    }
  }
}
</style>
