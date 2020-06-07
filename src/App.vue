<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="AddTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <br/>
    <Dones v-bind:dones="dones" v-on:del-done="deleteDone" />
    <!-- <Dones /> -->
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import Dones from './components/Dones';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo,
    Dones
  },
  data() {
    return {
      todos: [
      ],
      dones: [
        {
          id: 11,
          title: 'done task 1'
        },
        {
          id: 12,
          title: 'done task 2'
        }
      ]
    }
  },
  methods: {
      AddTodo(newTodo) {
        const {title, completed} = newTodo;
        axios.post('https://jsonplaceholder.typicode.com/todos', {
          title,
          completed
        })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(e=>console.log(e));
      },
      deleteTodo(id) {
        axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
        .then(
          // eslint-disable-next-line no-unused-vars
          res => {
            this.dones = [...this.dones, this.todos.filter(todo => todo.id == id)[0]];
            this.todos = this.todos.filter(todo => todo.id !== id);
          }
        )
        .catch(e => console.log(e));
      },
      deleteDone(id) {
        this.dones = this.dones.filter(done => done.id != id);
      }
    },
    created() {
        axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
          .then(res => this.todos = res.data)
          .catch(e => console.log(e));
      }
}
</script>

<style>
*{
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
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.bth:hover {
  background: #666;
}

</style>
