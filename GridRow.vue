<template>
  <div class="grid-row" :style="rowStyle">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'GridRow',
  props: {
    gutter: {
      type: [Number, String],
      default: 1 // in rem
    },
    align: {
      type: String,
      default: 'start', // vertical align
      validator: (val) => ['start', 'center', 'end', 'stretch'].includes(val)
    },
    justify: {
      type: String,
      default: 'start', // horizontal align
      validator: (val) =>
        ['start', 'center', 'end', 'space-between', 'space-around'].includes(
          val
        )
    }
  },
  computed: {
    rowStyle() {
      const gutter = isNaN(this.gutter) ? this.gutter : `${this.gutter}rem`
      return {
        display: 'grid',
        gridTemplateColumns: 'repeat(12, 1fr)',
        gap: gutter,
        alignItems: this.align,
        justifyContent: this.justify,
        gridAutoFlow: 'row'
      }
    }
  }
}
</script>

<style scoped>
.grid-row {
  width: 100%;
}
</style>
