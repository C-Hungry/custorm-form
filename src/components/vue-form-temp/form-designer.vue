<template>
  <div class="form-designer" v-on:drop="onDrop($event)" v-on:dragover="onDragOver($event)" v-on:dragleave="onDragLeave($event)">
    <div v-for="field in fields" class="form-designer-item" draggable="true" v-on:click="onItemClick(field,$event)" v-on:dragstart="onItemDragStart(field,$event)">
      <split v-if="field.drop=='before'"></split>
      <div class="form-designer-content" v-bind:class="current.field==field?'selected':''">
        <datebox v-if="field.type=='date'" :field="field"></datebox>
        <daterangebox v-else-if="field.type=='daterange'" :field="field"></daterangebox>
        <datetimebox v-else-if="field.type=='datetime'" :field="field"></datetimebox>
        <datetimerangebox v-else-if="field.type=='datetimerange'" :field="field"></datetimerangebox>
        <multiselectbox v-else-if="field.type=='multiselect'" :field="field"></multiselectbox>
        <numberbox v-else-if="field.type=='number'" :field="field"></numberbox>
        <photobox v-else-if="field.type=='photo'" :field="field"></photobox>
        <selectbox v-else-if="field.type=='select'" :field="field"></selectbox>
        <textbox v-else-if="field.type=='text'" :field="field"></textbox>
        <textareabox v-else-if="field.type=='textarea'" :field="field"></textareabox>
        <textnotebox v-else-if="field.type=='textnote'" :field="field"></textnotebox>
        <split v-else-if="field.type=='split'" :field="field"></split>
        <div class="form-designer-close" @click="deleteItem(field,$event)">x</div>
      </div>
      <split v-if="field.drop=='after'"></split>
      <div class="form-designer-layer" v-on:dragover="onItemDragOver(field,$event)" v-on:dragleave="onItemDragLeave(field,$event)" v-on:drop="onItemDrop(field,$event)"></div>
    </div>
    <split v-if="isAdd"></split>
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
  import textnotebox from "./form-item/form-item-textnote.vue"
  import split from "./form-item/form-split.vue"
  export default {
    components: {
      split,
      datebox,
      daterangebox,
      datetimebox,
      datetimerangebox,
      multiselectbox,
      numberbox,
      photobox,
      selectbox,
      textbox,
      textareabox,
      textnotebox
    },
    name: "form-designer",
    data() {
      return {
        isAdd: false,
      }
    },
    methods: {
      deleteItem(field, event) {
        var index = this.fields.indexOf(field);
        if (index >= 0) {
          this.fields.splice(index, 1);
        }
        if (this.current.field == field) this.current.field = null;
        event.cancelBubble = true;
      },
      onItemClick(field, event) {
        this.current.field = this.current.field != field ? field : null;
      },
      onItemDragStart(field, event) {
        window.__dragInHandField = field;
      },
      onItemDragOver(field, event) {
        event.cancelBubble = true;
        field.drop = event.offsetY > event.srcElement.offsetHeight / 2 ? "after" : "before";
        event.preventDefault();
      },
      onItemDragLeave(field, event) {
        field.drop = "";
      },
      onItemDrop(field, event) {
        event.cancelBubble = true;
        setTimeout(() => {
          field.drop = "";
          window.__dragInHandField = null;
        });
        if (field == window.__dragInHandField) return;
        var index1 = this.fields.indexOf(window.__dragInHandField);
        if (index1 >= 0) {
          this.fields.splice(index1, 1);
        }
        var index2 = this.fields.indexOf(field);
        if (index2 >= 0) {
          this.fields.splice(field.drop == 'after' ? index2 + 1 : index2, 0, window.__dragInHandField)
        }
      },
      onDragOver(event) {
        this.isAdd = true;
        event.preventDefault();
      },
      onDragLeave(event) {
        this.isAdd = false;
      },
      onDrop(event) {
        setTimeout(() => {
          this.isAdd = false;
          window.__dragInHandField = null;
        });
        var index = this.fields.indexOf(window.__dragInHandField);
        if (index >= 0) {
          this.fields.splice(index, 1);
        }
        this.fields.push(window.__dragInHandField);
      },
    },
    props: {
      current: {
        type: Object,
        default: {
          field: null
        }
      },
      fields: {
        type: Array,
        default: () => {
          return []
        },
      },
    }
  }
</script>

<style scoped lang="less">
  .form-designer {
    overflow-x: hidden;
    overflow-y: auto;
    .form-designer-item {
      position: relative;
      .form-designer-content {
        border: solid 1px rgba(0, 0, 0, 0);
        border-bottom: solid 1px rgba(0, 0, 0, 0.1);
        .form-designer-close {
          position: absolute;
          right: 0;
          top: 0;
          width: 16px;
          height: 16px;
          line-height: 16px;
          background-color: rgba(255, 0, 0, 0.8);
          color: #fff;
          text-align: center;
          display: none;
          z-index: 9;
          cursor: pointer;
        }
      }
      .form-designer-content.selected {
        border: solid 1px rgba(255, 0, 0, 0.8)!important;
      }
      .form-designer-layer {
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        opacity: 0;
        cursor: move;
      }
    }
    .form-designer-item:hover {
      .form-designer-content {
        border: dashed 1px rgba(255, 0, 0, 0.8);
        .form-designer-close {
          display: block;
        }
      }
    }
  }
</style>
