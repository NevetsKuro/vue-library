<template>
  <div class="dialog-position" @click="closeBackdrop">
    <div class="dialog-container" :style="`max-width: ${dialogWidth}`">
      <div class="close drip-text-button" @click="closeDialog">
        <b-icon-x scale="1.6" class="color-wealthy-green-500" />
      </div>
      <div class="dialog-content">
        <slot name="content"></slot>
        <div class="dialog-header">
          <slot name="header"></slot>
        </div>
        <div class="dialog-body">
          <slot name="body"></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showDialog: {
      type: Boolean,
      default: false
    },
    dialogWidth: {
      type: String,
      default: '480px'
    }
  },
  methods: {
    confirmDialog() {
      this.$emit('confirm')
    },
    closeBackdrop(e) {
      if (e.target && e.target.getAttribute('class') === 'dialog-position') {
        this.$emit('close')
      }
    },
    closeDialog() {
      this.$emit('close')
    }
  }
}
</script>
<style lang="scss" scoped>
.dialog-position {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1040;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #00000042;
  .dialog-container {
    background-color: $white;
    color: rgba(0, 0, 0, 0.87);
    -webkit-transition: box-shadow 300ms cubic-bezier(0.4, 0, 0.2, 1) 0ms;
    transition: box-shadow 300ms cubic-bezier(0.4, 0, 0.2, 1) 0ms;
    border-radius: 4px;
    box-shadow: 0px 11px 15px -7px rgb(0 0 0 / 20%),
      0px 24px 38px 3px rgb(0 0 0 / 14%), 0px 9px 46px 8px rgb(0 0 0 / 12%);
    margin: 32px;
    position: relative;
    overflow-y: auto;
    display: flex;
    -webkit-flex-direction: column;
    -ms-flex-direction: column;
    flex-direction: column;
    max-height: calc(100% - 64px);
    max-width: 480px;
    padding: 32px;
    padding-top: 64px;
    .close {
      position: absolute;
      top: 24px;
      right: 40px;
      opacity: 1 !important;
      font-weight: 400;
      font-size: 16px;
      color: $wealthy-green-500;
      cursor: pointer;
    }
    h4 {
      font-weight: 700;
      font-size: 24px;
      line-height: 33px;
    }
    p {
      font-weight: 400;
      font-size: 16px;
      line-height: 19px;
    }
  }
}
.dialog-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  .dialog-img {
    object-fit: cover;
    height: 170px;
    width: 480px;
    margin: auto;
  }
  .dialog-header {
    font-weight: 700;
    font-size: 24px;
    line-height: 28px;
    text-align: center;
    color: $noble-blue-500;
    margin-top: 24px;
    margin-bottom: 8px;
  }
  .dialog-body {
    font-weight: 400;
    font-size: 16px;
    line-height: 19px;
    text-align: center;
    color: $black;
    width: 90%;
    margin: auto;
    margin-bottom: 24px;
    white-space: pre-wrap;
  }
}
</style>
