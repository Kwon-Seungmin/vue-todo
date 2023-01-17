<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>
<script setup>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';
import { ref } from 'vue'

const todoItems = ref([]);

const addOneItem = (todoItem) => {
  const obj = {
    completed: false,
    item: todoItem
  }
  localStorage.setItem(todoItem.item, JSON.stringify(obj));
  todoItems.value.push(obj);
}
const removeOneItem = (todoItem, index) => {
  localStorage.removeItem(todoItem.item);
  todoItems.value.splice(index, 1);
}
const toggleOneItem = (todoItem, index) => {
  todoItems.value[index].completed = !todoItems.value[index].completed;
  localStorage.removeItem(todoItem.item.value);
  localStorage.setItem(todoItem.item.value, JSON.stringify(todoItem));
}
const clearAllItems = () => {
  localStorage.clear();
  todoItems.value = [];
}
const onCreated = () => {
  if (localStorage.length > 0) {
    for (let i = 0; i < localStorage.length; i++) {
      todoItems.value.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
    }
  }
}
onCreated();
</script>

<style>
body {
  text-align: center;
  background-color: #F6F6F6;
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
