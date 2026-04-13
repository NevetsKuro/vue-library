<template>
  <div
    class="alert"
    :class="[`alert-${type}`, { 'alert--with-subtitle': subtitle }]"
  >
    <div class="alert-icon" :class="`alert-icon--${type}`" aria-hidden="true">
      <div class="alert-icon__ring"></div>
      <div class="alert-icon__glyph">
        <!-- Success: checkmark (Figma Standard Alerts — Small/Large Success) -->
        <svg
          v-if="type === 'success'"
          class="alert-icon__svg"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M6 12.5l4 4 8-9"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
        <!-- Warning: triangle + exclamation (Figma Warning) -->
        <svg
          v-else-if="type === 'warning'"
          class="alert-icon__svg"
          viewBox="0 0 22 19"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M11 3.99L18.53 17H3.47L11 3.99ZM11 0L0 19H22L11 0ZM12 14H10V16H12V14ZM12 8H10V12H12V8Z"
            fill="currentColor"
          />
        </svg>
        <!-- Danger: X (Figma Error) -->
        <svg
          v-else-if="type === 'danger'"
          class="alert-icon__svg"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M8 8l8 8M16 8l-8 8"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
          />
        </svg>
        <!-- Info: lowercase i in circle context (Figma Info) -->
        <svg
          v-else
          class="alert-icon__svg"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <circle cx="12" cy="7" r="1.5" fill="currentColor" />
          <path fill="currentColor" d="M11 11h2v8h-2v-8z" />
        </svg>
      </div>
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
  gap: 0;
  color: $noble-blue-500;

  &--with-subtitle {
    align-items: flex-start;
  }

  &-success {
    background: $spring-green-100;
    border: 1px solid $spring-green-600;
  }

  &-warning {
    background: $mustard-yellow-100;
    border: 1px solid $mustard-yellow-500;
  }

  &-danger {
    background: $orange-100;
    border: 1px solid $orange-500;
  }

  &-info {
    background: $sky-blue-100;
    border: 1px solid $sky-blue-500;
  }
}

/* Figma: 24px white circle, 2px semantic border, ~14.4px glyph centered */
.alert-icon {
  position: relative;
  width: 24px;
  height: 24px;
  flex-shrink: 0;
  margin-right: 16px;
  display: grid;
  place-items: center;

  .alert--with-subtitle & {
    margin-top: 2px;
  }

  &__ring {
    grid-area: 1 / 1;
    width: 24px;
    height: 24px;
    box-sizing: border-box;
    border-radius: 50%;
    border: 2px solid transparent;
  }

  &__glyph {
    grid-area: 1 / 1;
    width: 14.4px;
    height: 14.4px;
    display: flex;
    align-items: center;
    justify-content: center;
    pointer-events: none;
  }

  &__svg {
    width: 100%;
    height: 100%;
    display: block;
    color: inherit;
  }

  &--success {
    color: $spring-green-600;
    .alert-icon__ring {
      border-color: $spring-green-600;
      background: $white;
    }
  }

  &--warning {
    color: $mustard-yellow-500;
    .alert-icon__ring {
      border-color: $mustard-yellow-500;
      background: $white;
    }
  }

  &--danger {
    color: $orange-500;
    .alert-icon__ring {
      border-color: $orange-500;
    }
  }

  &--info {
    color: $sky-blue-500;
    .alert-icon__ring {
      border-color: $sky-blue-500;
    }
  }
}

.alert-content {
  flex: 1;
  min-width: 0;
}

.alert-title {
  font-weight: 700;
  font-size: 16px;
  color: $noble-blue-500;
}

.alert-subtitle {
  margin-top: 8px;
  font-size: 14px;
  font-weight: 400;
  color: $noble-blue-500;
}
</style>
