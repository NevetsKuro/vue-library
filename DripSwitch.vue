<template>
  <div class="switch-container">
    <div
      :class="[
        'switch-button-container',
        switchState === 'on' ? 'on-state' : 'off-state'
      ]"
      @click="changeState()"
    >
      <div class="switch-circle-button"></div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['switchState', 'changeState']
}
</script>
<style lang="scss" scoped>
.switch-container {
  width: 100%;
  .switch-button-container {
    position: relative;
    border-radius: 75px;
    width: 40px;
    height: 20px;
    border: 1px solid $wealthy-green-500;
    background: $wealthy-green-500;
    padding: 3px;
    cursor: pointer;
    .switch-circle-button {
      position: absolute;
      width: 12px;
      height: 12px;
      background: $white;
      border-radius: 50%;
    }
    &.on-state {
      background: $wealthy-green-500;
      .switch-circle-button {
        background: $white;
        right: 4px;
      }
    }
    &.off-state {
      background: $white;
      .switch-circle-button {
        background: $wealthy-green-500;
        left: 4px;
      }
    }
  }
}
</style>
