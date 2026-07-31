<template>
  <div v-if="showDialog" class="dialog-position" @click="closeBackdrop">
    <div class="dialog-container" :style="`max-width: ${dialogWidth}`">
      <div class="dialog-content">
        <slot name="content"></slot>
        <!-- Header and close button share a row so the close aligns with the
             title rather than floating over the container corner. -->
        <div v-if="$slots.header || showClose" class="dialog-header-row">
          <div class="dialog-header">
            <slot name="header"></slot>
          </div>
          <div
            v-if="showClose"
            class="close drip-text-button"
            role="button"
            tabindex="0"
            aria-label="Close dialog"
            @click="closeDialog"
            @keydown.enter="closeDialog"
            @keydown.space.prevent="closeDialog"
          >
            <svg
              width="26"
              height="26"
              viewBox="0 0 24 24"
              fill="none"
              class="color-wealthy-green-500"
              xmlns="http://www.w3.org/2000/svg"
              aria-hidden="true"
            >
              <path
                d="M18 6L6 18M6 6l12 12"
                stroke="currentColor"
                stroke-width="1.75"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
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
    },
    // Set to false to hide the close button (e.g. a dialog the user must
    // resolve through its own actions).
    showClose: {
      type: Boolean,
      default: true
    }
  },
  mounted() {
    document.addEventListener('keydown', this.handleKeydown)
  },
  beforeDestroy() {
    document.removeEventListener('keydown', this.handleKeydown)
  },
  methods: {
    confirmDialog() {
      this.$emit('confirm')
    },
    closeBackdrop(e) {
      // Compare against currentTarget (the backdrop the listener is bound to)
      // rather than matching the class string exactly — callers may add their
      // own class (e.g. "steps-dialog") which Vue merges onto this root
      // element and would break an exact class-attribute match.
      if (e.target === e.currentTarget) {
        this.$emit('close')
      }
    },
    closeDialog() {
      this.$emit('close')
    },
    handleKeydown(e) {
      if (e.key === 'Escape' && this.showDialog) {
        this.$emit('close')
      }
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
    border-radius: 8px;
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
    padding: 16px 12px;
    .close {
      flex-shrink: 0;
      opacity: 1 !important;
      font-weight: 400;
      font-size: 16px;
      color: $wealthy-green-500;
      cursor: pointer;
      display: inline-flex;
      border-radius: 6px;

      &:focus-visible {
        outline: 2px solid $wealthy-green-500;
        outline-offset: 2px;
      }
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
  .dialog-header-row {
    display: flex;
    // Align to the first line, so headers that also carry a subtitle keep the
    // close button level with the title rather than centred on the block.
    align-items: flex-start;
    justify-content: space-between;
    gap: 16px;
    margin-top: 24px;
    margin-bottom: 8px;
  }
  .dialog-header {
    flex: 1;
    min-width: 0;
    font-weight: 700;
    font-size: 24px;
    line-height: 28px;
    text-align: center;
    color: $noble-blue-500;
  }
  .dialog-body {
    font-weight: 400;
    font-size: 16px;
    line-height: 19px;
    text-align: center;
    color: $black;
    width: 90%;
    margin: auto;
    margin-top: 12px;
    margin-bottom: 24px;
    white-space: pre-wrap;
  }
}
</style>
