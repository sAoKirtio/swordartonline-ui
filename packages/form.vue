<template>
  <div class="hm-form">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'SoForm',
  props: {
    model: {
      type: Object,
      required: true
    },
    labelWidth: {
      type: String,
      default: '80px'
    }
  },
  provide () {
    return {
      Form: this
    }
  }
}
</script>

<style>

</style>
