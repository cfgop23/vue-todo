<template>
  <div id="app">
   <TodoHeader/>
   <TodoInput v-on:addTodoItem="addOneItem"/>
   <TodoList 
    v-bind:propsData="todoItems" 
    v-on:removeItem="removeOneItem" 
    v-on:toggleItem="toggleOneItem"/>
   <TodoFooter v-on:clearAll="clearAllItems"/>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() {
    return {
      todoItems: [],
      index: 0
    }
  },
  methods: {
    addOneItem(todoItem) {
      this.index += 1;
      const obj = { completed: false, item: todoItem, index: this.index - 1};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem(todoItem, i) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(i, 1);
    },
    toggleOneItem(todoItem, i) {
      // todoItem.completed = !todoItem.completed;
      this.todoItems[i].completed = !this.todoItems[i].completed;
      // 로컬스토리지에 boolean 데이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems() {
      localStorage.clear();
      this.todoItems = [];
      this.index = 0;
    }
  },
  created() {
    if(!localStorage.length) return;
    for(let i = 0; i < localStorage.length; i++) {
      // this.todoItems.push(localStorage.key(i));
      this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
    }
    this.todoItems = this.todoItems.sort((a,b)=>(a.index - b.index));
    this.index = this.todoItems[this.todoItems.length -1].index + 1;
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  }
}
</script>

<style>
body {
  display: flex;
  justify-content: center;
  text-align: center;
  background-color: #f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 500px;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
