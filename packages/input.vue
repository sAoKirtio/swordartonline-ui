<template>
  <div class="so-input" :class="{'so-input--suffix':showSuffix}" :style="{width}">
    <input
    class="so-input__inner"
    :class="{'is-disabled':disabled}"
    :type="showPassword ? (passwordVisible? 'text':'password'):type"
    :placeholder="placeholder"
    :name="name"
    :value="value"
    :disabled="disabled"
    @input="handleInput"
    @focus="handleFocus"
    @blur="handleBlur"
    @change="handleChange"
    >
    <span class="so-input__suffix" v-if="showSuffix">
      <i class="so-input__icon so-icon-circle-close" v-if="clearable && value" @click="clear"></i>
      <i class="so-input__icon so-icon-view" :class="{'so-icon-view-active':passwordVisible}" v-if="showPassword && value" @click="show"></i>
    </span>
  </div>
</template>

<script>
export default {
  name: 'SoInput',
  data () {
    return {
      passwordVisible: false
    }
  },
  props: {
    placeholder: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    width: {
      type: String,
      default: '100%'
    },
    name: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    value: {
      type: String,
      default: ''
    },
    clearable: {
      type: Boolean,
      default: false
    },
    showPassword: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleInput (e) {
      this.$emit('input', e.target.value)
    },
    clear () {
      this.$emit('input', '')
    },
    show () {
      this.passwordVisible = !this.passwordVisible
    },
    handleFocus (e) {
      this.$emit('focus', e)
    },
    handleBlur (e) {
      this.$emit('blur', e)
    },
    handleChange (e) {
      this.$emit('change', e.target.value)
    }
  },
  computed: {
    showSuffix () {
      return this.clearable || this.showPassword
    }
  }
}
</script>

<style lang="scss">
.so-input {
  width: 100%;
  font-size: 14px;
  display: inline-block;
  position: relative;
  .so-input__inner {
    -webkit-appearance: none;
    background-color: #fff;
    background-image: none;
    border-radius: 4px;
    border: 1px solid #dcdfe6;
    box-sizing: border-box;
    color: #606266;
    display: inline-block;
    font-size: inherit;
    height: 40px;
    line-height: 40px;
    outline: none;
    padding: 0 15px;
    transition: border-color .2s cubic-bezier(.645,.045,.355,1);
    width: 100%;

    &:focus {
      outline: none;
      border-color: #409eff;
    }

    &.is-disabled {
      background-color: #f5f7fa;
      border-color: #e4e7ed;
      color: #c0c4cc;
      cursor: not-allowed;
    }

  }
}

.so-input--suffix {
  .so-input__inner {
    padding-right: 30px;
  }
  .so-input__suffix {
    position: absolute;
    height: 100%;
    right: 10px;
    top: 0;
    line-height: 40px;
    text-align: center;
    color: #c0c4cc;
    transition: all .3s;
    z-index: 900;
    i {
      color: #c0c4cc;
      font-size: 14px;
      cursor: pointer;
      transition: color .2s cubic-bezier(.645,.045,.355,1);
    }

    .so-icon-view-active {
      color: blue;
    }
  }
}
</style>
