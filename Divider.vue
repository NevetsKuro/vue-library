<template>
  <div
    class="rf-divider"
    :class="{
      'rf-divider--horizontal': orientation === 'horizontal',
      'rf-divider--vertical': orientation === 'vertical'
    }"
    :style="{
      ...{
        borderWidth:
          orientation === 'horizontal'
            ? `${thickness}px 0 0 0`
            : `0 ${thickness}px 0 0`
      },
      ..._sx
    }"
  />
</template>

<script>
export default {
  props: {
    thickness: {
      type: Number,
      default: 1
    },
    orientation: {
      type: String,
      default: 'horizontal',
      validator(val) {
        return ['horizontal', 'vertical'].includes(val)
      }
    },
    _sx: {
      type: Object,
      default: () => ({})
    }
  }
}
</script>

<style lang="scss" scoped>
.rf-divider {
  border-style: solid;
  border-color: $wealthy-green-500;

  &--horizontal {
    width: 100%;
  }

  &--vertical {
    height: 100%;
    width: 1px;
  }
}
</style>
