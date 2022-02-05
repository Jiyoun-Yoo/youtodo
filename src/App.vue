<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" 
              v-on:removeItem="removeOneItem" 
              v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="removeAllItems"></TodoFooter>
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
      todoItems: []
    }
  },
  methods: {
    addOneItem(todoItem) {
      const obj = { completed: false, item: todoItem };
      localStorage.setItem(todoItem, JSON.stringify(obj)); // key-value 형식 
      this.todoItems.push(obj);   
    },
    removeOneItem(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleOneItem(todoItem, index) {
      // todoItem.completed = !todoItem.completed; // props로 내린 아이템에 직접 접근하는 것은 바람직하지 않다.
      this.todoItems[index].completed = !this.todoItems[index].completed;

      // 로컬 스토리지의 데이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    removeAllItems() {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  // created() {
  //   // created는 인스턴스가 생성되자마자 일단 한번 실행된다.
  //   // TODO: vue의 life cycle 학습
  // },
  components: {
    // 컴포넌트 태그명 : 컴포넌트 내용

    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  }
}
</script>

<style>
/* 스타일을 지정하면 하위 컴포넌트까지 모두 적용 가능 */
body {
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
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
