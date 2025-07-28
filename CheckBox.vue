<template>
  <div class="form-check custom-checkbox-wrapper">
    <input
      :id="id"
      type="checkbox"
      :class="[
        'form-check-input',
        'custom-checkbox',
        isDisabled ? 'disabled' : ''
      ]"
      :checked="isChecked"
      :disabled="disabled"
      @change="isDisabled ? '' : $emit('input', $event.target.checked)"
    />
    <label class="form-check-label" :for="id">
      Accept Terms & conditions checkbox
    </label>
  </div>
</template>

<script>
export default {
  name: 'CheckBox',
  props: {
    id: {
      type: String,
      required: true
    },
    value: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    isChecked() {
      return this.value
    },
    isDisabled() {
      return !!this.disabled
    }
  }
}
</script>

<style lang="scss" scoped>
/* Hide default checkbox */
.custom-checkbox {
  position: absolute;
  opacity: 0;
  cursor: pointer;
}

/* Custom box */
.custom-checkbox + .form-check-label::before {
  content: '';
  display: inline-block;
  width: 24px; /* Size */
  height: 24px;
  border: 2px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
  vertical-align: middle;
  background-color: white;
  transition: all 0.2s ease;
}

/* Checked state */
.custom-checkbox:checked + .form-check-label::before {
  background-color: $wealthy-green-500; /* Custom color */
  border-color: $wealthy-green-500;
  &.disabled {
    background-color: $neutral-gray-500;
    border-color: $neutral-gray-500;
  }
}

/* Optional: check mark */
.custom-checkbox:checked + .form-check-label::after {
  content: '✔';
  position: absolute;
  left: 6px;
  top: 1px;
  font-size: 16px;
  color: white;
}

/* Positioning label text nicely */
.custom-checkbox-wrapper .form-check-label {
  display: flex;
  align-items: center;
  position: relative;
  line-height: 24px;
  user-select: none;
  cursor: pointer;
}
.disabled + .form-check-label {
  pointer-events: none;
}
</style>
