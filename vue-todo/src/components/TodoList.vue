<template>
  <div>
    <ul>
      <li v-for="(todoItem, i) in propsData" v-bind:key="todoItem.item" class="shadow">
        <i class="checkBtn fa-solid fa-square-check"
          v-bind:class="{checkBtnCompleted: todoItem.completed}" 
          v-on:click="toggleComplete(todoItem, i)" />
        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, i)">
          <i class="fa-solid fa-trash-can"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['propsData'],
  methods: {
    removeTodo: function (todoItem, i)  {
      this.$emit('removeItem', todoItem, i);
    },
    toggleComplete: function (todoItem, i) {
      this.$emit('toggleItem', todoItem, i);
    }
  },
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
  width: 500px;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  font-size: 1.2rem;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;

  cursor: pointer;
}
.checkBtn {
  line-height: 50px;
  color: #62acde;
  font-size: 1.3rem;
  margin-right: 10px;

  cursor: pointer;
}
.checkBtnCompleted {
  color: #b3adad;
  cursor: pointer;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
/* transition css */
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>