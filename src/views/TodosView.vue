<script setup>
import { uid } from 'uid'
import { ref, watch, computed } from 'vue';
import { Icon } from '@iconify/vue';
import TodosCreate from '../components/TodosCreate.vue';
import TodoItem from '../components/TodoItem.vue';

const todoList = ref([]);

console.log("shubham branch");

watch((todoList), () => {
  setTodoListLocalStorage();
}, {
  deep: true
})

const fetchTodoList = () => {
  const savedTodo = JSON.parse(localStorage.getItem("todoList"))
  if (savedTodo) {
    todoList.value = savedTodo
  }
}
fetchTodoList();


const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value))
}

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    isCompleted: false,
    isEdit: false,
    todo
  })
}

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
}
const handleEdit = (todoPos) => {
  todoList.value[todoPos].isEdit = !todoList.value[todoPos].isEdit;
}

const handleUpdate = (value, todoPos) => {
  todoList.value[todoPos].todo = value
}

const handleDelete = (id) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== id)
}

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted)
})

</script>

<template>
  <main>
    <h1>Create Todos</h1>
    <TodosCreate @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" @todo-toggle-complete="toggleTodoComplete"
        @todo-edit="handleEdit" @update-todo="handleUpdate" @delete-todo="handleDelete" />
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" color="#41b080" width="22" />
      <span>You have no todo's to complete! Add one!</span>
    </p>
    <p v-if="todoCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" color="#41b080" width="22" />
      <span>You have completed all your Todo</span>
    </p>

  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>