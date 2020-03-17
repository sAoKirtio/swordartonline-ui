<template>
  <div class="hm-checkbox-group">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'SoCheckboxGroup',
  props: {
    value: {
      type: Array
    }
  },
  provide () {
    return {
      CheckboxGroup: this
    }
  }
}
</script>

<style>

</style>
