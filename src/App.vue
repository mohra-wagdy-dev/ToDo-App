<script>
import ref from "vue"
export default{
   setup(){
   const todos= ref([])
   const newTodo= ref({})
 function create(){
  todos.value.push({
    id:Date.now(),
    content:newTodo.value,
    completed: false
  })
  newTodo.value=''
 }
   return{
    todos,
    newTodo,
    create
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

      <li v-for="item in todos" :key="item.id">
       <h3>{{ item.content }}</h3>
      </li>
    </ul>
    <div>
      <button class="footer">Select All</button>
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
  height: 100vh;
  padding: 10px;
  background: darkslategray;
}
.wrapper {
  background: #fff;
  max-width: 400px;
  margin: 120px auto;
  width: 100%;
  padding: 25px;
  border-radius: 5px;
  box-shadow: 0px 10px 15px black;
}
input {
  width: 97%;
  margin: 20px 0;
  height: 100%;
  border-radius: 3px;
  border: 1px solid #fcc;
  font-size: 17px;
  padding: 15px 5px;
  transition: all 0.3s ease;
}
form button {
  width: 100%;
  height: 100%;
  border: none;
  margin-left: 5px;
  color: #fff;
  font-size: 22px;
  outline: none;
  background: rgb(105, 4, 97);
  cursor: pointer;
  border-radius: 3px;
  pointer-events: none;
  transition: all 0.3s ease;
}
.wrapper .todolist {
  margin-top: 20px;
  max-height: 250px;
  overflow: auto;
}
.li {
  position: relative;
  list-style: none;
  margin-bottom: 8px;
  background: cadetblue;
  border-radius: 3px;
  padding: 10px 15px;
  cursor: default;
  overflow: hidden;
  word-wrap: break-word;
}
.footer {
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}
.footer button {
  padding: 6px 10px;
  border-radius: 7px;
  border: none;
  color: #fff;
  background-color: rgb(177, 126, 126);
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
.item {
  cursor: pointer;
}
</style>
