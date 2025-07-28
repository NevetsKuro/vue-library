<template>
  <div class="input-container">
    <div class="input-label">
      {{ label }}
    </div>
    <div class="input-block width-800">
      <input
        :id="id"
        :name="name"
        :data-vv-as="label"
        type="text"
        :placeholder="placeholder"
        v-validate="rules"
        v-model="inputValue"
        :class="{ 'input-error': errors.has(name) }"
      />
      <span v-if="errors.has(name)" class="error">
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
      default: 'inputId'
    },
    placeholder: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    },
    rules: {
      type: String,
      default: 'required'
    }
  },
  data() {
    return {
      inputValue: this.value
    }
  },
  watch: {
    inputValue(val) {
      this.$emit('input', val)
    },
    value(val) {
      this.inputValue = val
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
  color: red;
  font-size: 12px;
}
.input-container {
  width: 100%;
  margin-bottom: 16px;
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
      width: 400px;
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
      &.width-800 {
        width: 808px;
      }
      @media screen and (max-width: 768px) {
        width: 100%;
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
}
</style>
