<template>
  <div class="tab-container">
    <div
      v-for="tab in tabOptions"
      :class="['tab-button', tabSelected === tab ? 'active' : '']"
      :key="tab"
      @click="setTab(tab)"
    >
      {{ tab }}
    </div>
  </div>
</template>
<script>
export default {
  props: ['tabOptions', 'tabSelected', 'setTab']
}
</script>
<style lang="scss" scoped>
@import '../ui-library/assets/styles.scss';
.tab-container {
  display: flex;
  flex-direction: row;
  border-bottom: 1px solid grey;
  .tab-button {
    font-size: 14px;
    font-weight: 400;
    padding: 12px 18px;
    cursor: pointer;
    &.active {
      color: $wealthy-green-500;
      border-bottom: 2px solid $wealthy-green-500;
    }
    &:hover {
      background: $wealthy-green-50;
    }
  }
}
</style>
