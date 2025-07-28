<template>
  <div :class="columnClass" :style="colStyle">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'GridCol',
  props: {
    cols: Number,
    sm: Number,
    md: Number,
    lg: Number,
    xl: Number,

    order: Number,
    orderSm: Number,
    orderMd: Number,
    orderLg: Number,
    orderXl: Number
  },
  computed: {
    columnClass() {
      const col = this.cols ? `col-span-${this.cols}` : ''
      const sm = this.sm ? `sm:col-span-${this.sm}` : ''
      const md = this.md ? `md:col-span-${this.md}` : ''
      const lg = this.lg ? `lg:col-span-${this.lg}` : ''
      const xl = this.xl ? `xl:col-span-${this.xl}` : ''

      const order = this.order !== undefined ? `order-${this.order}` : ''
      const orderSm =
        this.orderSm !== undefined ? `sm:order-${this.orderSm}` : ''
      const orderMd =
        this.orderMd !== undefined ? `md:order-${this.orderMd}` : ''
      const orderLg =
        this.orderLg !== undefined ? `lg:order-${this.orderLg}` : ''
      const orderXl =
        this.orderXl !== undefined ? `xl:order-${this.orderXl}` : ''

      return [col, sm, md, lg, xl, order, orderSm, orderMd, orderLg, orderXl]
        .filter(Boolean)
        .join(' ')
    },
    colStyle() {
      return {} // Optional inline styles
    }
  }
}
</script>

<style scoped>
/* Column widths */
[class*='col-span-'] {
  grid-column: span var(--cols, 12) / span var(--cols, 12);
}
.col-span-1 {
  grid-column: span 1 / span 1;
}
.col-span-2 {
  grid-column: span 2 / span 2;
}
.col-span-3 {
  grid-column: span 3 / span 3;
}
.col-span-4 {
  grid-column: span 4 / span 4;
}
.col-span-5 {
  grid-column: span 5 / span 5;
}
.col-span-6 {
  grid-column: span 6 / span 6;
}
.col-span-7 {
  grid-column: span 7 / span 7;
}
.col-span-8 {
  grid-column: span 8 / span 8;
}
.col-span-9 {
  grid-column: span 9 / span 9;
}
.col-span-10 {
  grid-column: span 10 / span 10;
}
.col-span-11 {
  grid-column: span 11 / span 11;
}
.col-span-12 {
  grid-column: span 12 / span 12;
}

/* Ordering */
.order-0 {
  order: 0;
}
.order-1 {
  order: 1;
}
.order-2 {
  order: 2;
}
.order-3 {
  order: 3;
}
.order-4 {
  order: 4;
}
.order-5 {
  order: 5;
}
.order-6 {
  order: 6;
}
.order-7 {
  order: 7;
}
.order-8 {
  order: 8;
}
.order-9 {
  order: 9;
}
.order-10 {
  order: 10;
}

@media (min-width: 576px) {
  .sm\:col-span-1 {
    grid-column: span 1 / span 1;
  }
  .sm\:col-span-2 {
    grid-column: span 2 / span 2;
  }
  .sm\:col-span-3 {
    grid-column: span 3 / span 3;
  }
  .sm\:col-span-4 {
    grid-column: span 4 / span 4;
  }
  .sm\:col-span-5 {
    grid-column: span 5 / span 5;
  }
  .sm\:col-span-6 {
    grid-column: span 6 / span 6;
  }
  .sm\:col-span-7 {
    grid-column: span 7 / span 7;
  }
  .sm\:col-span-8 {
    grid-column: span 8 / span 8;
  }
  .sm\:col-span-9 {
    grid-column: span 9 / span 9;
  }
  .sm\:col-span-10 {
    grid-column: span 10 / span 10;
  }
  .sm\:col-span-11 {
    grid-column: span 11 / span 11;
  }
  .sm\:col-span-12 {
    grid-column: span 12 / span 12;
  }

  .sm\:order-0 {
    order: 0;
  }
  .sm\:order-1 {
    order: 1;
  }
  .sm\:order-2 {
    order: 2;
  }
  .sm\:order-3 {
    order: 3;
  }
}
@media (min-width: 768px) {
  .md\:col-span-1 {
    grid-column: span 1 / span 1;
  }
  .md\:col-span-2 {
    grid-column: span 2 / span 2;
  }
  .md\:col-span-3 {
    grid-column: span 3 / span 3;
  }
  .md\:col-span-4 {
    grid-column: span 4 / span 4;
  }
  .md\:col-span-5 {
    grid-column: span 5 / span 5;
  }
  .md\:col-span-6 {
    grid-column: span 6 / span 6;
  }
  .md\:col-span-7 {
    grid-column: span 7 / span 7;
  }
  .md\:col-span-8 {
    grid-column: span 8 / span 8;
  }
  .md\:col-span-9 {
    grid-column: span 9 / span 9;
  }
  .md\:col-span-10 {
    grid-column: span 10 / span 10;
  }
  .md\:col-span-11 {
    grid-column: span 11 / span 11;
  }
  .md\:col-span-12 {
    grid-column: span 12 / span 12;
  }
  .md\:order-1 {
    order: 1;
  }
  .md\:order-2 {
    order: 2;
  }
}
@media (min-width: 992px) {
  .lg\:col-span-1 {
    grid-column: span 1 / span 1;
  }
  .lg\:col-span-2 {
    grid-column: span 2 / span 2;
  }
  .lg\:col-span-3 {
    grid-column: span 3 / span 3;
  }
  .lg\:col-span-4 {
    grid-column: span 4 / span 4;
  }
  .lg\:col-span-5 {
    grid-column: span 5 / span 5;
  }
  .lg\:col-span-6 {
    grid-column: span 6 / span 6;
  }
  .lg\:col-span-7 {
    grid-column: span 7 / span 7;
  }
  .lg\:col-span-8 {
    grid-column: span 8 / span 8;
  }
  .lg\:col-span-9 {
    grid-column: span 9 / span 9;
  }
  .lg\:col-span-10 {
    grid-column: span 10 / span 10;
  }
  .lg\:col-span-11 {
    grid-column: span 11 / span 11;
  }
  .lg\:col-span-12 {
    grid-column: span 12 / span 12;
  }
  .lg\:order-1 {
    order: 1;
  }
}
@media (min-width: 1200px) {
  .xl\:col-span-1 {
    grid-column: span 1 / span 1;
  }
  .xl\:col-span-2 {
    grid-column: span 2 / span 2;
  }
  .xl\:col-span-3 {
    grid-column: span 3 / span 3;
  }
  .xl\:col-span-4 {
    grid-column: span 4 / span 4;
  }
  .xl\:col-span-5 {
    grid-column: span 5 / span 5;
  }
  .xl\:col-span-6 {
    grid-column: span 6 / span 6;
  }
  .xl\:col-span-7 {
    grid-column: span 7 / span 7;
  }
  .xl\:col-span-8 {
    grid-column: span 8 / span 8;
  }
  .xl\:col-span-9 {
    grid-column: span 9 / span 9;
  }
  .xl\:col-span-10 {
    grid-column: span 10 / span 10;
  }
  .xl\:col-span-11 {
    grid-column: span 11 / span 11;
  }
  .xl\:col-span-12 {
    grid-column: span 12 / span 12;
  }
  .xl\:order-1 {
    order: 1;
  }
}
</style>
