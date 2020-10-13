<template>
  <div>
  <div class="input-div">
    <input
      @keyup.enter="addItem()"
      class="inputText"
      type="text"
      v-model="todoModel"
      placeholder="type a dishes..."
    />
    <button>Add</button>
  </div>
    <div class="dishes">
      <dishes-list
        title="Ordered"
        :dishes-data="dishesOrderData"
        class="dishes-list"
        @dish-done="onOrdered"
      />
      <dishes-list
        title="Cooked"
        :dishes-data="dishesCookedData"
        class="dishes-list"
      />
      <dishes-list
        title="History"
        :has-action-buttons="false"
        :dishes-data="dishesHistoryData"
        class="dishes-list"
      />
    </div>
  </div>
</template>

<script>
import DishesList from './DishesList'
export default {
  name: 'Manager',

  components: {
    DishesList,
  },

  data() {
    return {
      dishesOrderData: [
        {
          id: 1,
          title: 'd11',
        },
        {
          id: 2,
          title: 'd22',
        },
        {
          id: 3,
          title: 'd33',
        },
        {
          id: 4,
          title: 'd44',
        },
        {
          id: 5,
          title: 'd5',
        },
      ],
      dishesCookedData: [],
      dishesHistoryData: [],
    }
  },

  methods: {
    onOrdered(id) {
      const index = this.dishesOrderData.findIndex((item) => item.id === id)
      if (index !== -1) {
        this.dishesCookedData.push(this.dishesOrderData[index])
        this.dishesOrderData.splice(index, 1)
      }
    },
  },
}
</script>

<style lang="css" scoped>
.dishes-list {
flex-grow: 1;
margin-right: 0.3em;
}
.dishes {
  display: flex;
}
.input-div {
  margin: 10px;
}
.input-div input {
width: 22em;
height: 1.5em;
}
.input-div button {
height: 1.9em;
}
</style>
