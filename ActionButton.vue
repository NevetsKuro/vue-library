<template>
  <b-button
    v-b-tooltip.hover
    :href="type === 'submit' ? '' : '#'"
    :type="type"
    class="rf-button"
    :class="[variant, size, extraClass]"
    @click="click"
    :title="bTitle"
  >
    <slot></slot>
  </b-button>
</template>
<script>
export default {
  props: {
    variant: {
      // solid, outline, text
      type: String,
      default: 'solid'
    },
    type: {
      // submit, reset, button
      type: String,
      default: 'button'
    },
    click: {
      type: Function,
      default: () => {
        return 1
      }
    },
    size: {
      // small, medium, large
      type: String,
      default: 'medium'
    },
    extraClass: {
      type: String,
      default: ''
    },
    bTitle: {
      type: String,
      default: ''
    }
  }
}
</script>
<style lang="scss" scoped>
.rf-button {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  font-weight: 700;
  height: 56px;
  border-radius: 8px;
  &.removeVerticalPadding {
    padding-left: 4px !important;
    padding-right: 4px !important;
  }
  &.fullWidth {
    width: 100%;
  }

  &.small {
    font-size: 12px;
    padding: 16px 8px;
  }
  &.medium {
    font-size: 16px;
    padding: 16px 32px;
  }
  &.large {
    font-size: 20px;
    padding: 16px 48px;
  }

  &:focus {
    box-shadow: 0 0 0 0.2rem #26b67f52 !important;
  }
  &.solid {
    background: $wealthy-green-500;
    border: 2px solid $wealthy-green-500;
    color: $white;
    &:active,
    &:hover {
      background: $wealthy-green-600 !important;
      color: $white !important;
      border-color: $wealthy-green-600 !important;
    }
    &.disabled {
      background: $neutral-gray-100;
      color: $neutral-gray-500;
      border: 2px solid $neutral-gray-100;
      &:hover {
        background: $neutral-gray-100 !important;
        color: $neutral-gray-500 !important;
        border-color: $neutral-gray-100 !important;
      }
    }
  }
  &.outline {
    border: 2px solid $wealthy-green-500;
    color: $wealthy-green-500;
    background: $white;
    &:active,
    &:hover {
      background: $wealthy-green-50 !important;
      color: $wealthy-green-600 !important;
      border-color: $wealthy-green-600 !important;
      outline: 0;
    }
  }
  &.text {
    border: 2px solid transparent;
    color: $wealthy-green-500;
    background: transparent;
    &:active,
    &:hover {
      background: $wealthy-green-50 !important;
      color: $wealthy-green-600 !important;
      border-color: $wealthy-green-50 !important;
      text-decoration: underline;
      outline: 0;
    }
  }
}
</style>
