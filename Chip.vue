<template>
  <div :class="['chip-wrapper', variant]">
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: {
    variant: {
      type: String,
      default: 'succes'
    } // success, warning, error, info
  }
}
</script>
<style lang="scss" scoped>
@import './../assets/scss/palette';
.chip-wrapper {
  display: flex;
  align-items: center;
  border: 1px solid $spring-green-400;
  background: $spring-green-50;
  padding: 4px 8px;
  border-radius: 1.5rem;
  width: -moz-max-content;
  white-space: nowrap;
  width: max-content;
  font-size: 10px;
  font-weight: 400;
  height: 20px;
  &.success {
    border: 1px solid $spring-green-400;
    background: $spring-green-50;
    color: $noble-blue-500;
  }
  &.warning {
    border: 1px solid $mustard-yellow-400;
    background: $mustard-yellow-50;
    color: $noble-blue-500;
  }
  &.error {
    border: 1px solid $orange-400;
    background: $orange-50;
    color: $noble-blue-500;
  }
  &.info {
    border: 1px solid $sky-blue-400;
    background: $sky-blue-50;
    color: $noble-blue-500;
  }
}
</style>
