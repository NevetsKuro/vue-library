<template>
  <div class="accordian-container">
    <div
      class="title-section d-flex align-items-center justify-content-between w-100"
      @click="open"
    >
      <div class="color-noble-blue-500">
        <b-icon-chevron-down
          class="mr-3 color-wealthy-green-500"
          :style="{ transform: isRotated ? 'rotate(180deg)' : 'rotate(0deg)' }"
        />
        <slot name="title-left"></slot>
      </div>
      <slot name="title-right"></slot>
    </div>
    <div v-if="openAccordian" class="body-section w-100">
      <slot name="body"></slot>
    </div>
  </div>
</template>
<script>
import { BIconChevronDown } from 'bootstrap-vue'

export default {
  components: {
    BIconChevronDown
  },
  data() {
    return {
      openAccordian: false,
      isRotated: false
    }
  },
  methods: {
    open() {
      this.isRotated = !this.isRotated
      this.openAccordian = !this.openAccordian
    }
  }
}
</script>
<style lang="scss" scoped>
.accordian-container {
  display: flex;
  flex-direction: column;
  font-weight: 700;
  font-size: 16px;
  line-height: 22px;
  color: $wealthy-green-500;
  border: 1px solid $sky-blue-500;
  border-radius: 8px;

  .title-section {
    padding: 12px 16px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
  }

  .body-section {
    padding: 12px 16px;
    color: $noble-blue-500;
    font-weight: 400;
    width: 100%;
  }
}

.color-noble-blue-500 {
  color: $noble-blue-500; /* replace with your desired color variable */
}

.mr-3 {
  margin-right: 1rem; /* 16px (usually equivalent to 1rem) */
}

.color-wealthy-green-500 {
  color: $wealthy-green-500; /* replace with your desired color variable */
}

.w-100 {
  width: 100%;
}

.d-flex {
  display: flex;
}

.align-items-center {
  align-items: center;
}

.justify-content-between {
  justify-content: space-between;
}
</style>
