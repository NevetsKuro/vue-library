<template>
  <div class="alert" :class="`alert-${type}`">
    <div class="alert-icon">
      <img
        v-if="type === 'success'"
        src="@/assets/images/common/checkmark-with-double-circle.svg"
        class="mr-2"
      />
      <img
        v-if="type === 'warning'"
        src="@/assets/images/common/exclamation-triangle.svg"
        class="mr-2"
      />
      <img
        v-if="type === 'info'"
        src="@/assets/images/common/exclamation-circle.svg"
        class="mr-2"
      />
      <img
        v-if="type === 'danger'"
        src="@/assets/images/common/cross-with-outline.svg"
        class="mr-2"
      />
    </div>
    <div class="alert-content">
      <div class="alert-title">{{ title }}</div>
      <div v-if="subtitle" class="alert-subtitle">{{ subtitle }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: 'info',
      validator: (value) =>
        ['info', 'success', 'warning', 'danger'].includes(value)
    },
    title: {
      type: String,
      required: true
    },
    subtitle: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss" scoped>
.alert {
  display: flex;
  align-items: center;
  padding: 16px;
  border-radius: 8px;
  color: $noble-blue-500;
  align-items: center;

  &-success {
    background: $spring-green-100;
    border: 2px solid $spring-green-600;
  }

  &-warning {
    background: $mustard-yellow-50;
    border: 2px solid $mustard-yellow-500;
  }

  &-danger {
    background: #f9eae9;
    border: 2px solid #e8c6c4;
  }
  &-info {
    background: $noble-blue-50;
    border: 2px solid $sky-blue-500;
  }
}

.alert-icon {
  margin-right: 16px;
}

.alert-content {
  flex: 1;
}

.alert-title {
  font-weight: 700;
  font-size: 16px;
  color: $noble-blue-500;
}

.alert-subtitle {
  font-size: 14px;
  color: $noble-blue-500;
}
</style>
