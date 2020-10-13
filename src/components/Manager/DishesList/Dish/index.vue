<template>
  <div class="container">
    <div>{{ title }}</div>
    <div v-if="hasAction">
      <button @click="onDone">
        Done
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dish',

  props: {
    title: {
      type: String,
      default: 'no title',
    },
    hasAction: {
      type: Boolean,
      default: true,
    },
  },

  methods: {
    onDone() {
      this.$emit('done')
    },
  },
}
</script>

<style lang="css" scoped>
.container {
  display: flex;
  justify-content: space-between;
}
</style>
