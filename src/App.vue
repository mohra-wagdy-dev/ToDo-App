<script>
import { ref } from "vue"
export default {
  setup() {
    const todos = ref([])
    const newTodo = ref("")
    function create() {
      todos.value.push({
        id: Date.now(),
        content: newTodo.value,
        completed: false
      })
      newTodo.value = ''
    }

    function remove(item) {
      todos.value.splice(todos.value.indexOf(item), 1)
    }
    function completed(item) {
      item.completed = !item.completed
    }
    function markAll() {
      todos.value.forEach((todo) => todo.completed = true)
    }
    return {
      todos,
      newTodo,
      create,
      remove,
      completed,
      markAll
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>TODO LIST:-</h1>
    <div>
      <form class="inputField" @submit.prevent="create">
        <input v-model="newTodo" type="text" autocomplete="off" />
        <button>Add</button>
      </form>
    </div>
    <ul class="todolist">
      <li v-for="item in todos" :key="item.id" class="todo-item">
        <h3 :class="{ done: item.completed }" @click="completed(item)">
          {{ item.content }}
        </h3>
        <button @click="remove(item)">delete</button>
      </li>
    </ul>
    <div>
      <button @click="markAll" class="footer">Select All</button>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}

body {
  width: 100%;
  min-height: 100vh;
  padding: 20px;
  background: linear-gradient(135deg, #4e54c8, #8f94fb);
  display: flex;
  justify-content: center;
  align-items: center;
}

.wrapper {
  background: rgba(255, 255, 255, 0.95);
  max-width: 500px;
  width: 100%;
  padding: 30px;
  border-radius: 20px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
  backdrop-filter: blur(10px);
}

h1 {
  color: #4e54c8;
  margin-bottom: 20px;
  font-size: 2.2em;
  font-weight: 700;
}

.inputField {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

input {
  width: 100%;
  height: 45px;
  border-radius: 8px;
  border: 2px solid #e0e0e0;
  font-size: 16px;
  padding: 0 15px;
  transition: all 0.3s ease;
  background: white;
}

input:focus {
  border-color: #4e54c8;
  outline: none;
  box-shadow: 0 0 10px rgba(78, 84, 200, 0.2);
}

form button {
  width: 100%;
  height: 45px;
  border: none;
  color: #fff;
  font-size: 16px;
  font-weight: 600;
  background: #4e54c8;
  cursor: pointer;
  border-radius: 8px;
  transition: all 0.3s ease;
}

form button:hover {
  background: #8f94fb;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(78, 84, 200, 0.3);
}

.todolist {
  margin: 25px 0;
  max-height: 350px;
  overflow-y: auto;
  padding: 0 5px;
}

.todolist::-webkit-scrollbar {
  width: 5px;
}

.todolist::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 25px;
}

.todolist::-webkit-scrollbar-thumb {
  background: #4e54c8;
  border-radius: 25px;
}

.todo-item {
  position: relative;
  list-style: none;
  margin-bottom: 12px;
  background: #f8f9fa;
  border-radius: 10px;
  padding: 15px 20px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s ease;
  border: 1px solid #eee;
}

.todo-item:hover {
  transform: translateX(5px);
  background: #fff;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
}

.todo-item h3 {
  margin: 0;
  font-size: 16px;
  color: #333;
  font-weight: 500;
  transition: all 0.3s ease;
}

.todo-item h3.done {
  text-decoration: line-through;
  color: #999;
}

.todo-item button {
  background: #ff6b6b;
  border: none;
  color: #fff;
  padding: 8px 15px;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 14px;
  font-weight: 500;
}

.todo-item button:hover {
  background: #ff4c4c;
  transform: scale(1.05);
}

.footer button {
  padding: 12px 25px;
  border-radius: 8px;
  border: none;
  color: #fff;
  background-color: #4e54c8;
  cursor: pointer;
  font-size: 15px;
  font-weight: 600;
  transition: all 0.3s ease;
  margin-top: 10px;
}

.footer button:hover {
  background-color: #8f94fb;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(78, 84, 200, 0.3);
}
</style>