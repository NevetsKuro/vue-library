<template>
  <div
    :id="id"
    :style="{
      display: 'flex',
      flexDirection: direction,
      flexWrap,
      flexBasis,
      flexGrow,
      flexShrink,
      alignContent,
      alignItems,
      alignSelf,
      justifyContent: justifyContent,
      justifySelf,
      padding: paddingSx,
      width,
      ...sx
    }"
    :class="className"
  >
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: {
    className: {
      type: String,
      default: ''
    },
    id: {
      type: String,
      default: ''
    },
    sx: {
      type: Object,
      default: () => {}
    },
    direction: {
      type: String,
      default: 'row'
    },
    flexBasis: {
      type: [String, Number],
      default: 'auto'
    },
    flexGrow: {
      type: Number,
      default: 0
    },
    flexShrink: {
      type: Number,
      default: 1
    },
    flexWrap: {
      type: String,
      default: 'nowrap'
    },
    alignContent: {
      type: String,
      default: 'normal'
    },
    alignItems: {
      type: String,
      default: 'normal'
    },
    alignSelf: {
      type: String,
      default: 'normal'
    },
    justifyContent: {
      type: String,
      default: 'normal'
    },
    justifySelf: {
      type: String,
      default: 'normal'
    },
    width: {
      type: String,
      default: 'auto'
    },
    paddingSx: {
      type: String,
      default: ''
    }
  }
}
</script>
