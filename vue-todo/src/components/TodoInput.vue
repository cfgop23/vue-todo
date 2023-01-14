<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keypress.enter="addTodo">
    <span class="addContainer shadow" v-on:click="addTodo">
      <i class="addBtn fa-solid fa-plus"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <!--
      you can use custom content here to overwrite
      default content
      -->
      <h3 slot="header">알림 <i class="fa-solid fa-xmark closeModalBtn" @click="showModal = false"></i></h3>
      <p slot="body">내용을 입력하세요.</p>
      <!-- <button slot="footer">확인</button> -->
    </Modal>
  </div>
</template>

<script>
import Modal from './common/AlertModal.vue'

export default {
  data: function () {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo: function() {
      if(this.newTodoItem) {
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      }
      else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function () {
      this.newTodoItem = "";
    },
  },
  components: {
    Modal
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
  font-size: 1.4rem;
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
.closeModalBtn {
  color: #42b983;
}
</style>