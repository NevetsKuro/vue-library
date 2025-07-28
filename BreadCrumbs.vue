<template>
  <div class="breadcrumb-container">
    <span class="page-item" @click="pageClick">{{ page }}</span>
    <template v-if="midSection !== ''">
      <b-icon-chevron-right class="breadcrumb-section" />
      <span
        class="ml-3"
        :class="disableMidLink ? '' : 'page-item'"
        @click="midSectionClick"
      >
        {{ midSection }}
      </span>
    </template>
    <b-icon-chevron-right class="breadcrumb-section" />
    <span class="breadcrumb-section"> {{ section }}</span>
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: {
    page: {
      type: String,
      default: ''
    },
    midSection: {
      type: String,
      default: ''
    },
    section: {
      type: String,
      default: 'solid'
    },
    disableMidLink: {
      type: Boolean,
      default: false
    },
    midSectionClick: {
      type: Function,
      default: () => {
        return 1
      }
    },
    pageClick: {
      type: Function,
      default: () => {
        return 1
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.breadcrumb-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  font-weight: 400;
  font-size: 16px;
  .breadcrumb-section {
    cursor: pointer;
    color: $wealthy-green-500;
    font-weight: 700;
    font-size: 16px;
    margin-left: 8px;
  }
  .page-item {
    cursor: pointer;
    &:hover {
      text-decoration: underline;
    }
  }
}
</style>
