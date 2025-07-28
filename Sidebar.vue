<template>
  <div
    class="sidebar-wrapper"
    :class="{
      'd-none': !isOpen,
      'd-block': isOpen
    }"
    @click="toggleSidebar()"
  >
    <!-- Sidebar -->
    <div
      class="sidebar bg-light border-right p-3"
      :class="{
        'left-side': leftSide,
        'right-side': rightSide
      }"
      @click.stop
    >
      <div class="close" @click.stop="toggleSidebar()">Close X</div>
      <slot name="sidebar-content">
        <h5>Sidebar</h5>
        <ul class="list-unstyled">
          <li><a href="#">Menu Item 1</a></li>
          <li><a href="#">Menu Item 2</a></li>
        </ul>
      </slot>
      <slot name="main-content"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
  props: ['isOpen', 'toggleSidebar', 'leftSide', 'rightSide']
}
</script>

<style lang="scss" scoped>
.sidebar-wrapper {
  min-height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.379);
  z-index: 1000;
  .sidebar {
    position: absolute;
    top: 0;
    width: 450px;
    min-height: 100vh;
    z-index: 1001;
    &.left-side {
      left: 0;
    }
    &.right-side {
      right: 0;
    }
  }
}

.border-right {
  border-right: 1px solid #dee2e6;
}

@media (max-width: 768px) {
  .sidebar {
    position: absolute;
    z-index: 1030;
    background-color: white;
    height: 100%;
    left: 0;
    top: 0;
  }
}
</style>
