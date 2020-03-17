<template>
  <div class="radio-group">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'SoRadioGroup',
  props: {
    value: null
  },
  provide () {
    return {
      RadioGroup: this
    }
  }
}
</script>

<style>

</style>
