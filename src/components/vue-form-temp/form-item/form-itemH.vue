<template>
  <div>
    <div class="form-item-fieldH">
      <div class="form-item-title">{{name}}：</div>
      <div class="form-item-value"></div>
    </div>
    <div class="form-item-fieldH">
      <div class="form-item-value" style="padding: 0 10px; line-height: 20px;">
        <slot name="default"></slot>
      </div>
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
.form-item-fieldH{
  min-height: 40px;
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
    line-height: 40px;
    position: relative;
    input[type=text],input[type=textarea],input[type=number],input[type=date],input[type=time],input[type=datetime-local],input[type=file],select,textarea{
      border: none;
      outline: none;
      margin: 0;
      padding: 0;
      height: 79px;
      width: 100%;
      background-color: rgba(0,0,0,0);
      color: #666;
    }
    select{
      opacity: 0;
    }
  }
}
</style>
