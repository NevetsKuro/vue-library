<template>
  <table class="table drip-library-table table-borderless">
    <thead class="drip-table-head">
      <tr class="drip-tr-class">
        <th
          v-for="field in computedFields"
          :key="field.key"
          @click="field.sortable ? sortBy(field.key) : null"
          style="cursor: pointer"
        >
          {{ field.label || field.key }}
          <span v-if="field.sortable && sortKey === field.key">
            {{ sortOrder === 'asc' ? '▲' : '▼' }}
          </span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in sortedItems" :key="index">
        <td v-for="field in computedFields" :key="field.key">
          {{ item[field.key] }}
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'SimpleTable',
  props: {
    items: {
      type: Array,
      required: true
    },
    fields: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      sortKey: '',
      sortOrder: 'asc'
    }
  },
  computed: {
    computedFields() {
      if (this.fields.length === 0 && this.items.length > 0) {
        return Object.keys(this.items[0]).map((key) => ({ key }))
      }

      return this.fields.map((field) =>
        typeof field === 'string' ? { key: field } : field
      )
    },
    sortedItems() {
      if (!this.sortKey) return this.items

      return [...this.items].sort((a, b) => {
        const aVal = a[this.sortKey]
        const bVal = b[this.sortKey]

        if (aVal === bVal) return 0

        const comparison = aVal > bVal ? 1 : -1
        return this.sortOrder === 'asc' ? comparison : -comparison
      })
    }
  },
  methods: {
    sortBy(key) {
      if (this.sortKey === key) {
        this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc'
      } else {
        this.sortKey = key
        this.sortOrder = 'asc'
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.drip-library-table {
  position: relative;
  border-collapse: separate;
  border-spacing: 0 4px;
  // table header
  .drip-table-head > tr {
    position: sticky;
    top: 0;
    z-index: 49;
    [aria-sort='none'] {
      background-image: url('./assets/sorting-none.svg') !important;
    }
    [aria-sort='ascending'] {
      background-image: url('./assets/sorting-ascending.svg') !important;
    }
    [aria-sort='descending'] {
      background-image: url('./assets/sorting-descending.svg') !important;
    }
    th {
      background: $sky-blue-50;
      border: 1px solid $sky-blue-400;
      border-width: 1px 0 1px 0;
      color: $noble-blue-500;
      font-style: normal;
      font-weight: 700;
      font-size: 12px;
      line-height: 16px;
      padding-top: 16px;
      padding-left: 16px !important;
      padding-bottom: 16px;
      vertical-align: middle;
    }
    th:first-child {
      border-width: 1px 0 1px 1px;
      border-top-left-radius: 8px;
      div {
        cursor: pointer;
      }
      .custom-control-label:before,
      .custom-control-label:after {
        top: 0px;
      }
    }
    th:last-child {
      border-width: 1px 1px 1px 0;
      border-top-right-radius: 8px;
    }
    .custom-control {
      min-height: 1rem;
    }
    .custom-control-input {
      height: 1rem;
    }
  }

  // table body
  tr {
    .currency-status {
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      padding-left: 4px;
      .title {
        font-weight: 400;
        font-size: 12px;
        line-height: 16px;
        color: $noble-blue-500;
        margin-bottom: 8px;
        letter-spacing: 0px !important;
        &.alternate {
          padding-bottom: 0px;
          margin-bottom: 8px;
          text-transform: initial;
          width: 104px;
        }
      }
      .checkbox-container {
        display: flex;
        .switch-button {
          padding: 2px;
          height: auto;
        }
      }
    }
    td {
      border: 1px solid $sky-blue-400;
      border-width: 1px 0px;
      font-style: normal;
      font-weight: 400;
      font-size: 12px;
      line-height: 16px;
      color: $noble-blue-500;
      vertical-align: middle;
      padding-top: 16px;
      padding-bottom: 16px;
      .custom-control-label::before,
      .custom-control-label::after {
        top: 0;
      }
    }
    td:first-child {
      border: 1px solid $sky-blue-400;
      border-width: 1px 0px 1px 1px;
      .drip-checkbox {
        top: 4px;
      }
    }
    td:nth-child(2) {
      font-style: normal;
      font-weight: 400;
      font-size: 12px;
      line-height: 16px;
      color: $noble-blue-500;
    }
    td:nth-child(3) {
      font-style: normal;
      font-weight: 400;
      font-size: 12px;
      line-height: 16px;
      color: $noble-blue-500;
    }
    td:last-child {
      border: 1px solid $sky-blue-400;
      border-width: 1px 1px 1px 0px;
    }
  }
}
</style>
