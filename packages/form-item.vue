<template>
   <div class="so-form-item">
    <label class="so-form-item__label" :style="{width:this.Form.labelWidth}">{{label}}</label>
    <div class="so-form-item__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SoFormItem',
  props: {
    label: String
  },
  inject: ['Form']
}
</script>

<style lang="scss">
.so-form-item {
  margin-bottom: 25px;
  .so-form-item__label {
    text-align: right;
    vertical-align: middle;
    float: left;
    font-size: 14px;
    color: #606266;
    line-height: 40px;
    padding: 0 12px 0 0;
    box-sizing: border-box;
  }
  .so-form-item__content {
    line-height: 40px;
    position: relative;
    font-size: 14px;
    overflow: hidden;
  }
}
</style>
