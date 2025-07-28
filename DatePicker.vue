<template>
  <div class="input-container">
    <div v-if="label" class="drip-label font-weight-400">{{ label }}</div>
    <div class="input-block">
      <input
        :id="id"
        :name="name"
        data-vv-as="Date"
        type="text"
        class="datera-datepicker"
        :placeholder="placeholder"
        :v-model="vModel"
        v-validate="'required|required_from'"
        value=""
        :disabled="disabled"
      />
      <svg
        name="calendar-icon"
        xmlns="http://www.w3.org/2000/svg"
        width="18"
        height="20"
        viewBox="0 0 11.92 13.244"
        class="svg-icon mr-3"
      >
        <path
          class="a"
          d="M6.973,7.96H5.649V9.284H6.973Zm2.649,0H8.3V9.284H9.622Zm2.649,0H10.946V9.284h1.324ZM13.6,3.324h-.662V2H11.609V3.324h-5.3V2H4.987V3.324H4.324A1.318,1.318,0,0,0,3.007,4.649L3,13.92a1.324,1.324,0,0,0,1.324,1.324H13.6A1.328,1.328,0,0,0,14.92,13.92V4.649A1.328,1.328,0,0,0,13.6,3.324Zm0,10.6H4.324V6.635H13.6Z"
          transform="translate(-3 -2)"
          fill="inherit"
        />
      </svg>
    </div>
  </div>
</template>

<script>
import '../views/AccountSummary/datera.min.js'
export default {
  name: 'DatePicker',
  props: {
    id: { type: String, default: '' },
    name: { type: String, default: '' },
    label: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: 'Select a date'
    },
    vModel: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  emits: ['update:modelValue', 'change', 'accept', 'error'],
  async mounted() {
    this.initDatepickers()
  },
  methods: {
    initDatepickers() {
      window.Datera = new window.Datera('datera-datepicker', {
        minYear: 2014,
        maxYear: new Date().getFullYear(),
        selectionType: 'single',
        theme: 'theme1-light',
        freezeDates: true
      })

      window.Datera.mount()
    }
  }
}
</script>

<style scoped lang="scss">
.input-container {
  width: fit-content;
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
    position: relative;
    .svg-icon {
      position: absolute;
      right: 4px;
      top: 18px;
      fill: $wealthy-green-500;
    }
    input {
      outline: 0px;
      max-width: 400px;
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
      &.width-800 {
        width: 808px;
      }
    }
  }
}
</style>
