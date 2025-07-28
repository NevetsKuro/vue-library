<template>
  <div>
    <div
      v-for="(option, index) in options"
      :key="index"
      class="form-check-container"
    >
      <input
        type="radio"
        class="form-check-input custom-radio"
        :id="`${name}-${index}`"
        :name="name"
        :value="option.value"
        v-model="selectedValue"
        v-validate="'required'"
        :data-vv-name="name"
        @keyup="$emit('keyup', $event)"
      />
      <label class="form-check-label" :for="`${name}-${index}`">
        {{ option.text }}
      </label>
    </div>

    <span class="text-danger" v-if="errors.has(name)">
      {{ errors.first(name) }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'RoutingRadioGroup',
  props: {
    value: {
      type: [String, Number],
      default: null
    },
    options: {
      type: Array,
      required: true
    },
    name: {
      type: String,
      required: true
    }
  },
  computed: {
    selectedValue: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      }
    }
  },
  inject: ['$validator']
}
</script>
<style lang="scss" scoped>
.form-check-container {
  display: block;
  position: relative;

  /* Hide native radio */
  .custom-radio {
    position: absolute;
    opacity: 0;
    cursor: pointer;
  }

  /* Custom circle */
  .custom-radio + .form-check-label::before {
    content: '';
    display: inline-block;
    width: 20px;
    height: 20px;
    border: 2px solid #ccc;
    border-radius: 50%;
    margin-right: 10px;
    vertical-align: middle;
    background-color: white;
    transition: all 0.2s ease;
  }

  /* Checked state circle */
  .custom-radio:checked + .form-check-label::before {
    border-color: $wealthy-green-500;
    background-color: $wealthy-green-500;
  }
  .custom-radio:hover + .form-check-label::before {
    border-color: $wealthy-green-600;
    background-color: $wealthy-green-600;
  }

  /* Inner dot when selected */
  .custom-radio:checked + .form-check-label::after,
  .custom-radio:hover + .form-check-label::after {
    content: '';
    position: absolute;
    left: 5px;
    top: 7px;
    width: 10px;
    height: 10px;
    background: white;
    border-radius: 50%;
  }
  .form-check-label,
  .custom-radio {
    cursor: pointer;
  }
}
</style>
