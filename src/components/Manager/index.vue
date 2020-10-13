<template>
  <div>
    <div class="input-div">
      <input
        ref="inputValue"
        @keyup.enter="addDish"
        type="text"
        placeholder="type a dishes..."
      />
      <button @click="addDish">Add</button>
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
        @dish-done="onCooked"
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
import DishesList from "./DishesList";
export default {
  name: "Manager",

  components: {
    DishesList,
  },

  data() {
    return {
      dishesOrderData: [],
      dishesCookedData: [],
      dishesHistoryData: [],
      counter: 0,
    };
  },

  methods: {
    onOrdered(id) {
      const index = this.dishesOrderData.findIndex((item) => item.id === id);
      if (index !== -1) {
        this.dishesCookedData.push(this.dishesOrderData[index]);
        this.dishesOrderData.splice(index, 1);
      }
    },
    onCooked(id) {
      const index = this.dishesCookedData.findIndex((item) => item.id === id);
      if (index !== -1) {
        this.dishesHistoryData.push(this.dishesCookedData[index]);
        this.dishesCookedData.splice(index, 1);
      }
    },
    addDish() {
      let value = this.$refs.inputValue.value;
      if (value) {
        this.counter += 1;
        this.dishesOrderData.push({ id: this.counter, title: value });
        this.$refs.inputValue.value = "";
      }
    },
  },
};
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
