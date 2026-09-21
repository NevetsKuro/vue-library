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
          <svg
            v-if="isOpen"
            class="action-input inverse"
            width="16"
            height="16"
            viewBox="0 0 16 16"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M13.28 5.96667L8.9333 10.3133C8.41997 10.8267 7.57997 10.8267 7.06664 10.3133L2.71997 5.96667"
              stroke="#121212"
              stroke-miterlimit="10"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
          <svg
            v-else
            class="action-input"
            width="16"
            height="16"
            viewBox="0 0 16 16"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M13.28 5.96667L8.9333 10.3133C8.41997 10.8267 7.57997 10.8267 7.06664 10.3133L2.71997 5.96667"
              stroke="#121212"
              stroke-miterlimit="10"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
          <!-- 
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
          /> -->
        </template>
      </multiselect>

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
  display: flex;
  align-items: center;
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
        line-height: 2.6rem;
        font-size: 1.2rem;
        border-bottom-right-radius: 5px;
        border-top-right-radius: 5px;
        top: 20px;
        right: 12px;
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
