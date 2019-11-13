This is the app component that holds all other components. This functions the same way that the App component in React would.


This Template is essentially the HTML for what will be shown on the page. In this case we have a div called app that contains everything. Inside of that div we are rendering the Todos component. The v-bind part is us passing down data to that component. We're passing down our todos data and telling the Todos component that the data is to be called "todos". The v-on del-todo is telling app what will happen when the del-todo event occurs. As we know from our other components, del-todo occurs when one of our buttons is clicked. When the event happens, we call the deleteTodo method.
<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

Here we are importing the Todos component so that we can pass data to it. In the export default,  we are naming this app component 'app', and exporting it so main.js can import it and render it to the dom via the public index.html file. The components part of export default tells us which subcomponents will be rendered by app. In this case, the Todos component. Finally, under data we create an array titled todos that we can pass to the Todos component via a v-bind. We can also put methods here.  Our method, deleteTodo filters through the array of Todos and filters out Todos that are clicked on. 
<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
// import axios from 'axios';
export default {
  name: 'app',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
},
    methods: {
      deleteTodo(id){
        this.todos = this.todos.filter(todo => todo.id !== id);
        },
        //This addTodo method takes our current todo list (...this.todos) and adds our newTodo
        addTodo(newTodo) {
          this.todos = [...this.todos, newTodo]
        }
      }
    }
        //Created is pretty much the same as componentDidMount Here we're telling the app theat when it loads in we want it to perform a get request from this API
  //       created() {
  //         axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
  //         .then(res => this.todos = res.data) 
  // }

</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding:0;
  }

  body {
    font-family:Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border:none;
    background: #555;
    color: #fff;
    padding:7px 20px;
    cursor:pointer;
  }
  btn:hover{
    background: #666;
  }
</style>
