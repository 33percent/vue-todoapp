<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos='todos' v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos.vue';
import AddTodo from '../components/AddTodo.vue';
import axios from 'axios';
export default {
  name: 'home',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos:[]
    }
  },
  methods:{
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(data => {
        this.todos = this.todos.filter(todo => todo.id !== id); 
      })
      .catch(err => {
        alert('cant delete')
      })
      
    },
    addTodo(obj) {
      const  { title, completed } = obj;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,completed
      })
      .then(data => {
        this.todos = [...this.todos, data.data];
      })
      .catch(err => {
        alert('faled to add')
      })
      // this.todos = [...this.todos, obj];
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(data => {
      this.todos = data.data;
    })
    .catch(err => {
      alert('fetch failed')
    })
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color:#fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
