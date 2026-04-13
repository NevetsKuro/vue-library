<template>
  <div
    :class="['link-button-card', isDisabled && 'link-button-card--disabled']"
    role="button"
    :tabindex="isDisabled ? -1 : 0"
    @click="onActivate"
    @keyup.enter.prevent="onActivate"
    @keyup.space.prevent="onActivate"
  >
    <span
      class="drip-body font-weight-700 color-noble-blue-500 link-button-card__label"
    >
      {{ label }}
    </span>
    <img
      src="@/assets/images/common/external-link-icon.svg"
      alt=""
      class="link-button-card__icon"
    />
  </div>
</template>

<script>
/**
 * Side “link” card: label + external-link affordance, permission-gated click.
 * Emits `click` when enabled; parent handles routing and analytics.
 */
export default {
  name: 'LinkButtonCard',
  props: {
    label: {
      type: String,
      required: true
    }
  },
  computed: {
    hasPermission() {
      return (
        this.$store.getters.hasPermission('esign') &&
        this.$store.getters.hasPermission('edit')
      )
    },
    isDisabled() {
      return !this.hasPermission
    }
  },
  methods: {
    onActivate() {
      if (this.isDisabled) return
      this.$emit('click')
    }
  }
}
</script>

<style lang="scss" scoped>
.link-button-card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px;
  background: $noble-blue-50;
  border: 1px solid $noble-blue-200;
  border-radius: 8px;
  width: 100%;
  cursor: pointer;

  &:hover {
    background: $noble-blue-100;
  }

  &--disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  &__label {
    flex: 1;
    min-width: 0;
  }

  &__icon {
    flex-shrink: 0;
    width: 24px;
    height: 24px;
    color: $noble-blue-500;
  }
}
</style>
