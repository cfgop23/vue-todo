<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer shadow" v-on:click="addTodo">
      <i class="addBtn fa-solid fa-plus"></i>
    </span>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function() {
      if(!this.newTodoItem) return;
      const obj = { completed: false, item: this.newTodoItem};
      localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
      this.clearInput();
    },
    clearInput: function () {
      this.newTodoItem = "";
    }
  }
}
</script>

<style scoped>
  input:focus {
  outline: none;
}
.inputBox {
  background: white;
  width: 100%;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  float: left;
  margin: 0 1rem;
  padding: 0;
  width: 420px;
  border-style: none;
  font-size: 1.5rem;
  line-height: 50px;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;

  cursor: pointer;
}
.addBtn {
  color: white;
  /* vertical-align: middle; */
}
</style>