<template>
  <div class="so-switch" @click="handleClick" :class="{'is-checked':value}">
    <span class="so-switch__core" ref="core">
      <span class="so-switch__button"></span>
    </span>
    <input
      class="so-switch__input"
      type="checkbox"
      ref="input"
      :name="name"
    >
  </div>
</template>

<script>
export default {
  name: 'SoSwitch',
  props: {
    value: {
      type: Boolean,
      default: false
    },
    activeColor: {
      type: String,
      default: ''
    },
    inactiveColor: {
      type: String,
      default: ''
    },
    name: {
      type: String,
      default: ''
    }
  },
  methods: {
    async handleClick () {
      this.$emit('input', !this.value)
      await this.$nextTick()
      this.setColor()
    },
    setColor () {
      if (this.activeColor || this.inactiveColor) {
        const color = this.value ? this.activeColor : this.inactiveColor
        this.$refs.core.style.borderColor = color
        this.$refs.core.style.backgroundColor = color
        this.$refs.input.checked = this.value
      }
    }
  },
  mounted () {
    this.setColor()
  }
}
</script>

<style lang="scss">
.so-switch {
  display: inline-flex;
  align-items: center;
  position: relative;
  font-size: 14px;
  line-height: 20px;
  height: 20px;
  vertical-align: middle;
  .so-switch__core {
    margin: 0;
    display: inline-block;
    position: relative;
    width: 40px;
    height: 20px;
    border: 1px solid #dcdfe6;
    outline: none;
    border-radius: 10px;
    box-sizing: border-box;
    background: #dcdfe6;
    cursor: pointer;
    transition: border-color .3s,background-color .3s;
    vertical-align: middle;
    .so-switch__button {
      position: absolute;
      top: 1px;
      left: 1px;
      border-radius: 100%;
      transition: all .3s;
      width: 16px;
      height: 16px;
      background-color: #fff;
    }
  }
}

.so-switch.is-checked {
  .so-switch__core {
    border-color: #409eff;
    background-color: #409eff;
    .so-switch__button {
      transform: translateX(20px);
    }
  }
}

.so-switch__input {
  position: absolute;
  width: 0;
  height: 0;
  opacity: 0;
  margin: 0;
}
</style>
