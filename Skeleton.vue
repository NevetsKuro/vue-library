<template>
  <div
    :class="['skeleton', variantClass, animationClass, className]"
    :style="customStyle"
  ></div>
</template>

<script>
export default {
  name: 'Skeleton',
  props: {
    animation: {
      type: String,
      default: 'pulse', // 'pulse' | 'wave' | false
      validator: (val) => ['pulse', 'wave', false].includes(val)
    },
    height: {
      type: [Number, String],
      default: null
    },
    width: {
      type: [Number, String],
      default: null
    },
    variant: {
      type: String,
      default: 'text' // 'text' | 'rectangular' | 'circular'
    },
    _sx: {
      type: Object,
      default: () => ({})
    },
    className: {
      type: String,
      default: ''
    }
  },
  computed: {
    animationClass() {
      return this.animation ? `skeleton--${this.animation}` : ''
    },
    variantClass() {
      return `skeleton--${this.variant}`
    },
    customStyle() {
      return {
        height:
          typeof this.height === 'number' ? `${this.height}px` : this.height,
        width: typeof this.width === 'number' ? `${this.width}px` : this.width,
        ...this._sx
      }
    }
  }
}
</script>

<style scoped>
.skeleton {
  background-color: #e0e0e0;
  border-radius: 4px;
  display: inline-block;
}

/* Variants */
.skeleton--text {
  height: 1em;
  width: 100%;
  border-radius: 4px;
}
.skeleton--rectangular {
  border-radius: 4px;
}
.skeleton--circular {
  border-radius: 50%;
}

/* Animations */
.skeleton--pulse {
  animation: pulse 1.5s infinite ease-in-out;
}

.skeleton--wave {
  position: relative;
  overflow: hidden;
}
.skeleton--wave::after {
  content: '';
  position: absolute;
  top: 0;
  left: -150px;
  height: 100%;
  width: 150px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.3),
    transparent
  );
  animation: wave 1.6s infinite;
}

@keyframes pulse {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.4;
  }
  100% {
    opacity: 1;
  }
}

@keyframes wave {
  0% {
    left: -150px;
  }
  100% {
    left: 100%;
  }
}
</style>
