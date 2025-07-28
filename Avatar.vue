<template>
  <div class="company-avatar">
    {{ getStartCase(companyName) }}
  </div>
</template>

<script>
export default {
  name: 'Avatar',
  props: {
    companyName: {
      type: String,
      required: true
    }
  },
  methods: {
    getStartCase(name) {
      const names = name.split(' ')
      let res = ''
      if (names.length > 1) {
        res = names[0].slice(0, 1) + names[names.length - 1].slice(0, 1) || ''
      } else {
        res = names[0].slice(0, 2)
      }
      return res.toUpperCase()
    }
  }
}
</script>

<style lang="scss" scoped>
.company-avatar {
  width: 80px;
  height: 80px;
  padding: 18px 19px;
  max-width: fit-content;
  gap: 0px;
  border-radius: 10px;
  border: 2px solid $sky-blue-500;
  font-size: 32px;
  font-weight: 700;
  line-height: 43.65px;
  text-align: center;
  color: $sky-blue-500;
  background-color: $sky-blue-50;
}
</style>
