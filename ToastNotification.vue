<template>
  <notifications
    position="top right"
    class="notification-toast"
    :duration="5000"
  >
    <template slot="body" slot-scope="props">
      <div class="custom-template" :class="props.item.type">
        <div class="custom-template-icon" :class="props.item.type">
          <b-icon-check-circle
            v-if="props.item.type === 'success'"
            class="icon"
          />
          <b-icon-exclamation-circle
            v-if="props.item.type === 'error'"
            class="icon"
          />
          <b-icon-exclamation-triangle
            v-if="props.item.type === 'warn'"
            class="icon"
          />
        </div>
        <div class="custom-template-content">
          <div class="custom-template-title">
            {{ props.item.title }}
          </div>
          <div v-if="props.item.text" class="custom-template-subtitle">
            {{ props.item.text }}
          </div>
        </div>
        <div
          class="custom-template-close"
          :class="props.item.type"
          @click="props.close"
        >
          <b-icon-x scale="1.5" />
        </div>
      </div>
    </template>
  </notifications>
</template>
<script>
export default {
  name: 'App'
}
</script>
<style lang="scss" scoped>
.notification-toast {
  z-index: 1020;
  width: 450px !important;
  @media screen and (max-width: 1023px) {
    width: 320px !important;
  }
  @media screen and (max-width: 576px) {
    width: 240px !important;
  }
  top: 80px !important;
}
.custom-template {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: flex-start;
  border-radius: 8px;
  text-align: left;
  font-size: 13px;
  margin: 5px;
  margin-bottom: 0;
  padding: 18px;
  opacity: 0.8;
  &,
  & > div {
    box-sizing: border-box;
  }
  &.success {
    background: $spring-green-100;
    border: 2px solid $spring-green-600;
  }
  &.error {
    background: #f9eae9;
    border: 2px solid #e8c6c4;
  }
  &.warn {
    background: $mustard-yellow-50;
    border: 2px solid $mustard-yellow-500;
  }
  .custom-template-icon {
    border: 2px solid transparent;
    border-radius: 50px;
    min-width: 24px;
    width: 24px;
    height: 24px;
    display: flex;
    align-items: center;
    justify-items: center;
    .icon {
      margin: auto;
      width: 12px;
      height: 12px;
    }
    &.success {
      color: $spring-green-600;
      border-color: $spring-green-600;
    }
    &.error {
      color: $danger;
      border-color: $danger;
    }
    &.warn {
      color: $mustard-yellow-500;
      border-color: $mustard-yellow-500;
    }
  }
  .custom-template-close {
    font-size: 16px;
    opacity: 1;
    margin-left: 16px;
    cursor: pointer;
    align-self: flex-start;
    color: $wealthy-green-500;
    &.success {
      color: $wealthy-green-500;
    }
    &.error {
      color: $danger;
    }
    &.warn {
      color: $mustard-yellow-500;
    }
  }
  .custom-template-content {
    flex: 1;
    margin-left: 10px;
    .custom-template-title {
      font-style: normal;
      font-weight: 700;
      font-size: 14px;
      line-height: 19px;
      display: flex;
      align-items: center;
    }
    .custom-template-subtitle {
      font-style: normal;
      font-weight: 400;
      font-size: 12px;
      line-height: 19px;
      display: flex;
      align-items: center;
    }
  }
}
</style>
