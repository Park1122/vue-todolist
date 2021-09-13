<template>
  <div>
    <todo-header></todo-header>
    <todo-input v-on:add="addTodoItem"></todo-input>
    <todo-list :todolist="todoItems" @remove="removeTodoItem"></todo-list>
    <todo-footer @clear="removeAllItems"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  components: {
    TodoHeader, TodoInput, TodoList,TodoFooter
  },
  data() {
    return {
      todoItems: []
    };
  },
  methods: {
    fetchTodoItems() {
      for(let i = 0; i < localStorage.length; i++) {
        let item = localStorage.key(i);
        this.todoItems.push(item);
      }
    },
    addTodoItem(value) {
      this.todoItems.push(value);
      localStorage.setItem(value, value);
    },
    removeTodoItem(todo, index) {
      this.todoItems.splice(index, 1);
      localStorage.removeItem(todo);
    },
    removeAllItems() {
      this.todoItems = [];
      localStorage.clear;
    }
  },
  created() {
    this.fetchTodoItems();
  }
}
</script>

<style>
</style>
