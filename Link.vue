<template>
  <a
    :href="disabled ? undefined : href"
    class="common-link"
    v-bind="$attrs"
    :target="target"
    :rel="rel"
    :style="_sx"
    @click="handleClick"
  >
    <slot></slot>
  </a>
</template>

<script>
export default {
  name: 'CommonLink',
  inheritAttrs: false,
  props: {
    href: {
      type: String,
      default: '#'
    },
    target: {
      type: String,
      default: '_self'
    },
    rel: {
      type: String,
      default: 'noopener noreferrer'
    },
    onClick: {
      type: Function,
      default: null
    },
    disabled: {
      type: Boolean,
      default: false
    },
    _sx: {
      type: Object,
      default: () => ({})
    }
  },
  methods: {
    handleClick(event) {
      if (this.disabled || this.href === '#') {
        event.preventDefault()
      }

      if (this.onClick) {
        this.onClick(event)
      }
    }
  }
}
</script>

<style scoped lang="scss">
.common-link {
  color: $wealthy-green-500;
  text-decoration: none;
  cursor: pointer;

  &:hover {
    text-decoration: underline;
  }

  &.is-disabled {
    pointer-events: none;
    color: $noble-blue-200;
    opacity: 0.6;
  }
}
</style>
