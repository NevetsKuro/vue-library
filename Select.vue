<template>
  <div class="input-container">
    <div class="input-label">
      {{ label }}
    </div>
    <div v-if="helpText" class="expandable-section">
      {{ helpText }}
    </div>
    <div class="input-block">
      <multiselect
        :id="name"
        :name="name"
        :data-vv-as="label"
        :placeholder="placeholder"
        v-model="currencyValue"
        v-validate="rules"
        :class="computedClasses"
        :style="{ width: inputWidth }"
        :options="options"
        :track-by="trackBy || undefined"
        :label="optionLabel || undefined"
        :allow-empty="allowEmpty"
        :show-labels="false"
        selectLabel=""
        selectedLabel=""
        deselectLabel=""
        @open="isOpen = true"
        @close="isOpen = false"
      >
        <template v-slot:singleLabel="{ option }">
          <slot name="singleLabel" :option="option">{{
            optionLabel && option ? option[optionLabel] : option
          }}</slot>
        </template>

        <template slot="option" slot-scope="{ option }">
          <slot name="option" :option="option">{{
            optionLabel && option ? option[optionLabel] : option
          }}</slot>
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
      type: [String, Object],
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
    trackBy: {
      type: String,
      default: ''
    },
    optionLabel: {
      type: String,
      default: ''
    },
    allowEmpty: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      isOpen: false,
      currencyValue: this.value
    }
  },
  computed: {
    computedClasses() {
      return ['drip-dropdown', { 'read-only': this.readonly }]
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
    .drip-dropdown {
      height: 56px;
      @media screen and (max-width: 768px) {
        width: 100% !important;
      }
      &.read-only {
        cursor: not-allowed;
        pointer-events: none;
        // Block interaction without vue-multiselect's `disabled` prop (which
        // adds .multiselect--disabled and a mismatched look vs TextField)
        ::v-deep .multiselect__tags {
          background-color: $neutral-gray-50;
          border: 1px solid $noble-blue-500;
          padding-right: 16px;
          cursor: not-allowed;
          pointer-events: none;
          &:hover {
            border: 1px solid $noble-blue-500;
            cursor: not-allowed;
          }
          .multiselect__single {
            color: $neutral-gray-600;
            background: transparent;
          }
        }
        ::v-deep .multiselect__select {
          display: none;
        }
        .action-input {
          display: none;
        }
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
