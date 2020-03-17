<template>
 <label class="so-radio" :class="{'is-checked':label === model}">
    <span class="so-radio__input">
      <span class="so-radio__inner"></span>
      <input
        class="so-radio__original"
        type="radio"
        :name="name"
        :value="label"
        v-model="model"
      >
    </span>
    <span class="so-radio__label">
      <slot></slot>
      <template v-if="!$slots.default">{{label}}</template>
    </span>
  </label>
</template>

<script>
export default {
  name: 'SoRadio',
  props: {
    label: {
      type: [String, Number, Boolean],
      default: ''
    },
    name: {
      type: String,
      default: ''
    },
    value: null
  },
  computed: {
    model: {
      get () {
        return this.isGroup ? this.RadioGroup.value : this.value
      },
      set (value) {
        this.isGroup ? this.RadioGroup.$emit('input', value) : this.$emit('input', value)
      }
    },
    isGroup () {
      // 用于判断是否有so-radio-group组件
      return !!this.RadioGroup
    }
  },
  inject: {
    RadioGroup: {
      default: ''
    }
  }
}
</script>

<style lang="scss">
.so-radio {
  color: #606266;
  font-weight: 500;
  line-height: 1;
  position: relative;
  cursor: pointer;
  display: inline-block;
  white-space: nowrap;
  outline: none;
  font-size: 14px;
  margin-right: 30px;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  .so-radio__input {
    white-space: nowrap;
    cursor: pointer;
    outline: none;
    display: inline-block;
    line-height: 1;
    position: relative;
    vertical-align: middle;
    .so-radio__inner {
      border: 1px solid #dcdfe6;
      border-radius: 100%;
      width: 14px;
      height: 14px;
      background-color: #fff;
      position: relative;
      cursor: pointer;
      display: inline-block;
      box-sizing: border-box;
      &:after {
        width: 4px;
        height: 4px;
        border-radius: 100%;
        background-color: #fff;
        content: "";
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%,-50%) scale(0);
        transition: transform .15s ease-in;
      }
    }
    .so-radio__original {
      opacity: 0;
      outline: none;
      position: absolute;
      z-index: -1;
      top: 0;
      left: 0px;
      right: 0;
      bottom: 0;
      margin: 0;
    }
  }
  .so-radio__label {
    font-size: 14px;
    padding-left: 10px;
  }
}

.so-radio.is-checked {
  .so-radio__input {
    .so-radio__inner {
      border-color: #409eff;
      background: #409eff;
      &:after {
        transform: translate(-50%,-50%) scale(1);
      }
    }
  }
  .so-radio__label {
    color: #409eff;
  }
}
</style>
