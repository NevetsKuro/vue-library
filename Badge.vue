<template>
  <div class="badge-wrapper">
    <slot />
    <span class="badge" :style="{ backgroundColor: backgroundColor }">
      {{ badgeContent }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'Badge',
  props: {
    badgeContent: {
      type: [String, Number],
      required: true
    },
    backgroundColor: {
      type: String,
      default: '#217DE5' // from your screenshot
    }
  }
}
</script>

<style scoped lang="scss">
.badge-wrapper {
  position: relative;
  display: inline-block;
}

.badge {
  position: absolute;
  top: -4px;
  right: -4px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 20px;
  min-width: 20px;
  padding: 0 6px;
  font-size: 12px;
  font-weight: 600;
  color: white;
  background-color: $noble-blue-300;
  border-radius: 10px;
  line-height: 1;
  white-space: nowrap;
}
</style>
