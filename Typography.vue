<template>
  <component
    :is="currentTag"
    :id="id"
    :class="[className, computedVariant, computedColor]"
    :style="{
      fontWeight,
      textTransform,
      textAlign,
      ...sx
    }"
  >
    <slot></slot>
  </component>
</template>
<script>
export default {
  props: {
    currentTag: {
      type: String,
      default: 'div'
    },
    className: {
      type: String,
      default: ''
    },
    sx: {
      type: String,
      default: ''
    },
    id: {
      type: String,
      default: ''
    },
    variant: {
      type: String,
      default: ''
    },
    color: {
      type: String,
      default: ''
    },
    fontWeight: {
      type: String,
      default: ''
    },
    textTransform: {
      type: String,
      default: ''
    },
    textAlign: {
      type: String,
      default: ''
    }
  },
  computed: {
    computedVariant() {
      return `drip-${this.variant}`
    },
    computedColor() {
      return `color-${this.color}`
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../ui-library/assets/styles.scss';
</style>
