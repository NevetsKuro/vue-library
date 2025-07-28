<template>
  <div :class="['circular-progress', className]" :data-testid="dataTestId">
    <svg
      :width="size"
      :height="size"
      viewBox="0 0 44 44"
      class="circular-svg"
      :class="{ spinning: variant === 'indeterminate' }"
    >
      <circle
        class="circular-bg"
        cx="22"
        cy="22"
        r="20.2"
        fill="none"
        :stroke-width="thickness"
      />
      <circle
        class="circular-fg"
        :class="{
          indeterminate: variant === 'indeterminate' && !disableShrink
        }"
        cx="22"
        cy="22"
        r="20.2"
        fill="none"
        :stroke-width="thickness"
        :stroke-dasharray="dashArray"
        :stroke-dashoffset="dashOffset"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'CircularProgress',
  props: {
    className: {
      type: String,
      default: ''
    },
    _sx: {
      type: Object,
      default: () => ({}) // Will be deprecated
    },
    value: {
      type: Number,
      default: 0
    },
    variant: {
      type: String,
      default: 'indeterminate', // or 'determinate'
      validator: (v) => ['determinate', 'indeterminate'].includes(v)
    },
    disableShrink: {
      type: Boolean,
      default: false
    },
    size: {
      type: [Number, String],
      default: 40
    },
    thickness: {
      type: Number,
      default: 3.6
    },
    dataTestId: {
      type: String,
      default: ''
    }
  },
  computed: {
    dashArray() {
      return 2 * Math.PI * 20.2
    },
    dashOffset() {
      if (this.variant === 'determinate') {
        const progress = this.value / 100
        return this.dashArray * (1 - progress)
      }
      return 0
    }
  }
}
</script>

<style scoped lang="scss">
.circular-progress {
  display: inline-block;
  position: relative;
}

.circular-svg {
  transform-origin: center;
}

.circular-svg.spinning {
  animation: spin 2s linear infinite;
}

.circular-bg {
  stroke: #e0e0e0;
}

.circular-fg {
  stroke: $wealthy-green-500;
  transition: stroke-dashoffset 0.3s;
}

.circular-fg.indeterminate {
  animation: dash 1.5s ease-in-out infinite;
}

@keyframes spin {
  100% {
    transform: rotate(360deg);
  }
}

@keyframes dash {
  0% {
    stroke-dasharray: 1, 200;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 100, 200;
    stroke-dashoffset: -15px;
  }
  100% {
    stroke-dasharray: 1, 200;
    stroke-dashoffset: -125px;
  }
}
</style>
