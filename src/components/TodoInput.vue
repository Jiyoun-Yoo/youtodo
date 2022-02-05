<template>
  <div class="inputBox shadow"> 
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>

    <Modal v-if="showModal" @click="showModal=false">
      <h3 slot="header">
        Warning!
      </h3>
      <div slot="body">
        내용이 입력되지 않았습니다.
      </div>
      <div slot="footer">
        <i class="closeBtn far fa-times-circle" @click="showModal=false"></i>
      </div>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false,
    }
  },
  methods: {
    addTodo() {
      if(this.newTodoItem !== '') {
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      // input box 초기화
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
  }
}
</script>

<style scoppped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 1rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #ff5e5e, #cc0707ec);
  display: black;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #afafaf;
}
</style>