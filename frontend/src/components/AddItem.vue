<template>
  <div>
    <form>
      <input
        id="todoInput"
        ref="todoInput"
        v-model="newTodo"
        @keydown.enter="itemAdded(newTodo)"
        placeholder="What to do?"
        type="text"
      />
      <button @click="itemAdded(newTodo)" type="submit" id="addButton">
        Add Item
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  async mounted() {
    this.$refs["todoInput"].focus();
  },
  data() {
    return {
      newTodo: "",
    };
  },
  methods: {
    itemAdded(newTodo) {
      console.log(newTodo);
      axios.post("/api/todo-items", {
        text: `${newTodo}`,
        done: false,
      });
      this.$refs["todoInput"].value = "";
    },
  },
};
</script>

<style>
form {
  display: flex;
  justify-content: center;
  margin-bottom: 2rem;
}
input {
  width: 25%;
  height: 2rem;
  font-size: 20px;
}
input:focus {
  outline-width: 0;
}
</style>
