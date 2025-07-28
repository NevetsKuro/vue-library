<template>
  <div class="input-container">
    <div class="input-label">
      {{ label }}
    </div>
    <div class="input-block width-800">
      <multiselect
        :id="name"
        :name="name"
        :data-vv-as="label"
        :placeholder="placeholder"
        v-model="currencyValue"
        v-validate="rules"
        class="drip-dropdown"
        :options="options"
        :show-labels="false"
        selectLabel=""
        selectedLabel=""
        deselectLabel=""
        @open="isOpen = true"
        @close="isOpen = false"
      >
        <template slot="option" slot-scope="{ option }">
          {{ option }}
        </template>

        <template slot="caret">
          <img
            v-if="isOpen"
            src="@/assets/images/icons/chevron-down.svg"
            alt="caret"
            class="action-input"
          />
          <img
            v-else
            src="@/assets/images/icons/chevron-down.svg"
            alt="caret"
            class="action-input inverse"
          />
        </template>
      </multiselect>

      <span v-if="errors.has(name)" class="error">
        {{ errors.first(name) }}
      </span>
    </div>
  </div>
</template>

<script>
import Multiselect from 'vue-multiselect'

export default {
  name: 'CurrencySelect',
  components: { Multiselect },
  props: {
    label: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: 'Enter...'
    },
    value: {
      type: String,
      default: ''
    },
    options: {
      type: Array,
      required: true
    },
    name: {
      type: String,
      default: 'currency'
    },
    rules: {
      type: String,
      default: 'required'
    }
  },
  data() {
    return {
      isOpen: false,
      currencyValue: this.value
    }
  },
  watch: {
    currencyValue(val) {
      this.$emit('input', val) // Enables v-model syncing
    },
    value(val) {
      this.currencyValue = val
    }
  },
  inject: ['$validator']
}
</script>

<style lang="scss" scoped>
@import '~vue-multiselect/dist/vue-multiselect.min.css';

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
    .drip-dropdown {
      height: 56px;
      width: 400px;
      @media screen and (max-width: 768px) {
        width: 100%;
      }
      .action-input {
        position: absolute;
        cursor: pointer;
        right: 0;
        padding-left: 1rem;
        padding-right: 1rem;
        line-height: 2.6rem;
        font-size: 1.2rem;
        border-bottom-right-radius: 5px;
        border-top-right-radius: 5px;
        top: 1.6rem;
        &.inverse {
          transform: rotate(180deg);
        }
      }
      ::v-deep .multiselect__select {
        height: 100%;
        width: 20px;
        margin-right: 8px;
        padding: 0px;
        &::before {
          z-index: 1;
        }
      }
      ::v-deep .multiselect__tags {
        outline: 0px;
        height: 56px;
        padding: 16px;
        padding-right: 36px;
        border-radius: 8px;
        border: 1px solid $noble-blue-500;
        color: $noble-blue-500;
        margin-bottom: 4px;
        .multiselect__placeholder {
          color: $neutral-gray-500;
          margin-top: -2px;
          padding-top: 0px;
          padding-left: 5px;
          font-size: 16px;
        }
        .multiselect__single {
          color: $noble-blue-500;
          font-weight: 700;
          vertical-align: bottom;
          width: 90% !important;
        }
        &:hover {
          border: 1px solid $noble-blue-300; // or a hover-specific color
          cursor: pointer;
        }
      }
      ::v-deep .multiselect__option {
        background-color: white;
        color: $noble-blue-500;
      }
      ::v-deep .multiselect__option--highlight {
        background-color: white;
        color: $noble-blue-500;
      }
      ::v-deep .multiselect__option--selected {
        background-color: white;
      }
      ::v-deep .multiselect__option:hover {
        background-color: $sky-blue-50;
        color: $wealthy-green-600;
      }
      ::v-deep .multiselect__content-wrapper {
        border: 1px solid $noble-blue-50;
        box-shadow: 0px 6px 12px 0px #0a2e5733;
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
