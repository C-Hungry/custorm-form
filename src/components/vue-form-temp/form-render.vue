<template>
  <div class="form-render">
    <div v-for="field in fields" class="form-designer-item">
      <div class="form-designer-content">
        <datebox v-if="field.type=='date'" :field="field" ></datebox>
        <daterangebox v-else-if="field.type=='daterange'" :field="field" ></daterangebox>
        <datetimebox v-else-if="field.type=='datetime'" :field="field" ></datetimebox>
        <datetimerangebox v-else-if="field.type=='datetimerange'" :field="field" ></datetimerangebox>
        <multiselectbox v-else-if="field.type=='multiselect'" :field="field" ></multiselectbox>
        <numberbox v-else-if="field.type=='number'" :field="field" ></numberbox>
        <photobox v-else-if="field.type=='photo'" :field="field" :onPhotoUploading="onPhotoUploading" :onPhotoUploaded="onPhotoUploaded" :onPhotoUploadFailed="onPhotoUploadFailed"></photobox>
        <selectbox v-else-if="field.type=='select'" :field="field" ></selectbox>
        <textbox v-else-if="field.type=='text'" :field="field" ></textbox>
        <textareabox v-else-if="field.type=='textarea'" :field="field" ></textareabox>
      </div>
    </div>
  </div>
</template>

<script>
import datebox from "./form-item/form-item-date.vue"
import daterangebox from "./form-item/form-item-daterange.vue"
import datetimebox from "./form-item/form-item-datetime.vue"
import datetimerangebox from "./form-item/form-item-datetimerange.vue"
import multiselectbox from "./form-item/form-item-multiselect.vue"
import numberbox from "./form-item/form-item-number.vue"
import photobox from "./form-item/form-item-photo.vue"
import selectbox from "./form-item/form-item-select.vue"
import textbox from "./form-item/form-item-text.vue"
import textareabox from "./form-item/form-item-textarea.vue"
import split from "./form-item/form-split.vue"
export default {
  components: {
    split,
    datebox,daterangebox,datetimebox,datetimerangebox,multiselectbox,numberbox,photobox,selectbox,textbox,textareabox,
  },
  name: "form-render",
  data () {
    return {}
  },
  props:{
    fields:{
      type: Array,
      default: ()=>{
        return [];
      },
    },
    onPhotoUploading: {
      type: Function,
      default: () => {},
    },
    onPhotoUploaded: {
      type: Function,
      default: () => {},
    },
    onPhotoUploadFailed: {
      type: Function,
      default: () => {},
    },
  }
}
</script>

<style scoped lang="less">
.form-render{
  overflow-y: auto;
  overflow-x: hidden;
  .form-designer-item{
    position: relative;
    .form-designer-content{
      border: solid 1px rgba(0, 0, 0, 0);
      border-bottom: solid 1px rgba(0, 0, 0, 0.1);
    }
  }
}
</style>
