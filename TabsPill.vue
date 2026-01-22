<template>
  <div class="tabs-pill" role="tablist">
    <button
      v-for="tab in tabs"
      :key="tab.value || tab.label"
      class="tabs-pill__tab"
      :class="{
        'is-active': isActive(tab),
        'is-disabled': isDisabled(tab)
      }"
      type="button"
      role="tab"
      :aria-selected="isActive(tab)"
      :aria-disabled="isDisabled(tab)"
      @click="selectTab(tab)"
    >
      <div class="tabs-pill__content">
        <span v-if="tab.icon" class="tabs-pill__icon">
          <img :src="tab.icon" :alt="tab.label" width="20" height="20" />
        </span>
        <component
          v-else-if="tab.iconComponent"
          :is="tab.iconComponent"
          class="tabs-pill__icon"
        />
        <span class="tabs-pill__label drip-label">{{ tab.label }}</span>
        <span v-if="hasBadge(tab)" class="tabs-pill__badge drip-label">
          {{ tab.badge }}
        </span>
      </div>
    </button>
  </div>
</template>

<script>
export default {
  name: 'TabsPill',
  model: {
    prop: 'value',
    event: 'input'
  },
  props: {
    /**
     * Array of tab objects: { label, value, icon?, iconComponent?, badge?, disabled? }
     */
    tabs: {
      type: Array,
      required: true
    },
    value: {
      type: [String, Number, Boolean, Object],
      default: null
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    isActive(tab) {
      return tab.value === this.value
    },
    isDisabled(tab) {
      return this.disabled || tab.disabled
    },
    hasBadge(tab) {
      return tab.badge !== undefined && tab.badge !== null
    },
    selectTab(tab) {
      if (this.isDisabled(tab)) {
        return
      }
      if (!this.isActive(tab)) {
        this.$emit('input', tab.value)
      }
      this.$emit('change', tab)
    }
  }
}
</script>

<style scoped lang="scss">
.tabs-pill {
  display: flex;
  align-items: stretch;
  width: 72%;
  @media screen and (max-width: $laptop) {
    width: 100%;
  }
  border-bottom: 1px solid $sky-blue-200;
}

.tabs-pill__tab {
  outline: 0;
  flex: 1;
  background: $white;
  border: 1px solid $sky-blue-200;
  border-right: 0;
  padding: 14px 24px;
  cursor: pointer;
  transition: background-color 0.15s ease, border-color 0.15s ease,
    color 0.15s ease, box-shadow 0.15s ease;
  color: $secondary;
  font-weight: 600;
  text-align: left;
  border-radius: 12px 12px 0 0;

  &:first-child {
    border-top-left-radius: 12px;
    border-bottom-left-radius: 0;
    border-left: 1px solid $sky-blue-200;
  }

  &:last-child {
    border-right: 1px solid $sky-blue-200;
    border-top-right-radius: 12px;
    border-bottom-right-radius: 0;
  }

  &.is-active {
    background: $noble-blue-500;
    color: $white;
    border-color: $noble-blue-500;
    box-shadow: 0 3px 10px rgba(10, 46, 87, 0.18);
    z-index: 1;

    .tabs-pill__badge {
      background: $noble-blue-200;
      color: $white;
    }
  }

  &.is-disabled {
    cursor: not-allowed;
    opacity: 0.6;
  }

  &:hover:not(.is-disabled):not(.is-active) {
    background: $sky-blue-50;
  }
}

.tabs-pill__content {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
}

.tabs-pill__icon {
  background: white;
  border-radius: 8px;
  display: inline-flex;
  width: 24px;
  height: 24px;
  align-items: center;
  justify-content: center;

  img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }
}

.tabs-pill__badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 32px;
  height: 32px;
  padding: 0 10px;
  border-radius: 16px;
  background: $sky-blue-300;
  color: $white;
  font-weight: 700;
}

@media screen and (max-width: $laptop) {
  .tabs-pill__tab {
    padding: 12px 54px;
  }
}
</style>
