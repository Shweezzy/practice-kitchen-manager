<template>
  <div class="container">
    <div class="title">
      {{ title }}
    </div>
    <div>
      <div v-if="isEmpty">
        The list is empty
      </div>
      <div v-if="!isEmpty">
        <dish
          v-for="item in dishesData"
          :key="item.id"
          :title="item.title"
          :has-action="hasActionButtons"
          class="dish"
          @done="onDone(item.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Dish from './Dish'
export default {
  name: 'DishesList',
  components: {
    Dish,
  },

  props: {
    title: {
      type: String,
      default: 'No title',
    },
    hasActionButtons: {
      type: Boolean,
      default: true,
    },
    dishesData: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    isEmpty() {
      return !this.dishesData || this.dishesData.length === 0
    },
  },

  methods: {
    onDone(id) {
      this.$emit('dish-done', id)
    },
  },
}
</script>

<style lang="css" scoped>
.container {
  padding: 10px;
  background-color: rgb(202, 224, 217);
  border: 1px solid rgb(0, 0, 8);
  border-radius: 8px;
}
.title {
  font-size: 32px;
  margin: 22px 0px 22px 0px;
}
.dish {
  margin-bottom: 10px;
}
</style>
