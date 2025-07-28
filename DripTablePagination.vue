<template>
  <nav>
    <ul class="pagination">
      <li class="page-item" :class="{ disabled: currentPage === 1 }">
        <button class="page-link" @click="selectPage(currentPage - 1)">
          «
        </button>
      </li>

      <li
        v-for="page in pageCount"
        :key="page"
        class="page-item"
        :class="{ active: currentPage === page }"
      >
        <button class="page-link" @click="selectPage(page)">
          {{ page }}
        </button>
      </li>

      <li class="page-item" :class="{ disabled: currentPage === pageCount }">
        <button class="page-link" @click="selectPage(currentPage + 1)">
          »
        </button>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'SimplePagination',
  props: {
    totalRows: {
      type: Number,
      required: true
    },
    perPage: {
      type: Number,
      default: 20
    },
    value: {
      type: Number,
      default: 1
    } // v-model compatible
  },
  computed: {
    pageCount() {
      return Math.ceil(this.totalRows / this.perPage)
    },
    currentPage: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      }
    }
  },
  methods: {
    selectPage(page) {
      if (page >= 1 && page <= this.pageCount) {
        this.currentPage = page
      }
    }
  }
}
</script>
