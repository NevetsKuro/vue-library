<template>
  <div class="input-container">
    <div class="input-label">
      {{ label }}
    </div>
    <div v-if="helpText" class="expandable-section">
      {{ helpText }}
    </div>
    <div class="input-block">
      <input
        :id="id || name"
        :name="name"
        :data-vv-as="label"
        type="text"
        :placeholder="placeholder"
        v-validate="rules"
        :data-vv-validate-on="validateOn"
        v-model="inputValue"
        :class="{ 'input-error': errors.has(name) }"
        :style="{ width: inputWidth }"
        :readonly="readonly"
        @blur="onBlur"
      />
      <span v-if="errors.has(name)" class="error">
        <svg
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M14.3733 7.15997L13.4733 6.10664C13.3067 5.90664 13.1667 5.5333 13.1667 5.26664V4.1333C13.1667 3.42664 12.5867 2.84664 11.88 2.84664H10.7467C10.48 2.84664 10.1 2.70664 9.9 2.53997L8.84667 1.63997C8.38667 1.24664 7.63334 1.24664 7.17334 1.63997L6.10667 2.53997C5.90667 2.70664 5.53334 2.84664 5.26667 2.84664H4.11334C3.40667 2.84664 2.82667 3.42664 2.82667 4.1333V5.26664C2.82667 5.52664 2.69334 5.89997 2.52667 6.09997L1.62667 7.15997C1.24 7.62664 1.24 8.3733 1.62667 8.82664L2.52667 9.88664C2.69334 10.08 2.82667 10.46 2.82667 10.72V11.86C2.82667 12.5666 3.40667 13.1466 4.11334 13.1466H5.27334C5.53334 13.1466 5.91334 13.2866 6.11334 13.4533L7.16667 14.3533C7.62667 14.7466 8.38 14.7466 8.84 14.3533L9.89334 13.4533C10.0933 13.2866 10.4667 13.1466 10.7333 13.1466H11.8667C12.5733 13.1466 13.1533 12.5666 13.1533 11.86V10.7266C13.1533 10.46 13.2933 10.0866 13.46 9.88664L14.36 8.8333C14.7667 8.37997 14.7667 7.62664 14.3733 7.15997ZM7.5 5.41997C7.5 5.14664 7.72667 4.91997 8 4.91997C8.27334 4.91997 8.5 5.14664 8.5 5.41997V8.63997C8.5 8.9133 8.27334 9.13997 8 9.13997C7.72667 9.13997 7.5 8.9133 7.5 8.63997V5.41997ZM8 11.2466C7.63334 11.2466 7.33334 10.9466 7.33334 10.58C7.33334 10.2133 7.62667 9.9133 8 9.9133C8.36667 9.9133 8.66667 10.2133 8.66667 10.58C8.66667 10.9466 8.37334 11.2466 8 11.2466Z"
            fill="#A94C2D"
          />
        </svg>
        {{ errors.first(name) }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CustomInput',
  props: {
    label: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    id: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: ''
    },
    value: {
      type: [String, Number],
      default: ''
    },
    rules: {
      type: String,
      default: 'required'
    },
    helpText: {
      type: String,
      default: ''
    },
    inputWidth: {
      type: String,
      default: '400px'
    },
    readonly: {
      type: Boolean,
      default: false
    },
    validateOn: {
      type: String,
      default: 'input|blur'
    }
  },
  data() {
    return {
      inputValue: this.value != null ? String(this.value) : ''
    }
  },
  watch: {
    inputValue(val) {
      this.$emit('input', val)
    },
    value(val) {
      this.inputValue = val != null ? String(val) : ''
    }
  },
  methods: {
    onBlur(e) {
      this.$validator.validate(this.name)
      this.$emit('blur', e)
    }
  },
  inject: ['$validator']
}
</script>

<style lang="scss" scoped>
.input-error {
  border-color: red;
}
.error {
  display: flex;
  align-items: center;
  gap: 4px;
  color: red;
  font-size: 12px;
}
.input-container {
  width: 100%;
  margin-bottom: 16px;

  &:focus-within {
    .expandable-section {
      max-height: 100px;
      opacity: 1;
      margin-top: 10px;
      margin-bottom: 8px;
    }
  }

  .input-label {
    font-size: 14px;
    font-weight: 400;
    line-height: 19px;
    letter-spacing: 0em;
    text-align: left;
    color: $noble-blue-500;
    margin-bottom: 8px;
  }
  .input-block {
    display: flex;
    flex-direction: column;

    input:-webkit-autofill,
    input:-webkit-autofill:hover,
    input:-webkit-autofill:focus,
    input:-webkit-autofill:active {
      -webkit-box-shadow: 0 0 0 30px white inset !important;
    }
    input {
      outline: 0px;
      height: 56px;
      padding: 16px;
      border-radius: 8px;
      border: 1px solid $noble-blue-500;
      color: $noble-blue-500;
      font-size: 16px;
      font-weight: 700;
      &::placeholder {
        font-weight: 400;
        color: $neutral-gray-500;
      }
      &:active,
      &:focus {
        border: 1px solid $noble-blue-300;
      }
      &[readonly] {
        background-color: $neutral-gray-50;
        color: $neutral-gray-600;
        cursor: not-allowed;
        &:active,
        &:focus {
          border: 1px solid $noble-blue-500;
        }
      }
      &.width-800 {
        width: 808px !important;
      }
      @media screen and (max-width: 768px) {
        width: 100% !important;
      }
    }
    .error {
      color: $red-400;
      font-size: 12px;
      font-weight: 400;
      line-height: 16px;
      letter-spacing: 0em;
      text-align: left;
      margin-top: 8px;
      @media screen and (max-width: 768px) {
        margin-top: 2px;
      }
    }
  }

  .expandable-section {
    max-height: 0;
    opacity: 0;
    overflow: hidden;
    transition: all 0.8s ease-in-out;
    max-width: 400px;
    font-size: 12px;
    padding-left: 8px;
    margin-bottom: 0px;
    color: $noble-blue-500;
    border-left: 4px solid $noble-blue-400;
  }
}
</style>
