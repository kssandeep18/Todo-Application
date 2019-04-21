<template>
  <div id="app" class="container">
    <h1 class="center">Todo App</h1><br/>
    <display-todos :todos=todos @deleteTodo="deleteTodo($event)"></display-todos>
    <add-todo @addTodo="addTodo($event)"></add-todo>
  </div>
</template>

<script>
import DisplayTodos from "./components/DisplayTodos";
import AddTodo from "./components/AddTodo"
export default {
  name: 'app',
  components: {
    "display-todos": DisplayTodos,
    "add-todo": AddTodo
  },
  data() {
    return {
      todos:[
        {id:1,content:"To drink water"},
        {id:2, content:"To complete assignment"}
      ]
    }
  },
  methods: {
    addTodo: function(newTodo) {
      let newId;
      if(this.todos.length===0) {
        newId=0;
      }
      else {
        newId=(this.todos[this.todos.length-1].id)+1;
      }
      let todosAfterInsertion=[...this.todos,{id:newId,content:newTodo}];
      this.todos=todosAfterInsertion;
    },
    deleteTodo: function(idToRemove) {
      let todosAfterDeletion=this.todos.filter(todo=> {
        if(todo.id!==parseInt(idToRemove)) {
          return true;
        }
        return false;
      });
      this.todos=todosAfterDeletion;
    }
  }
}
</script>

<style>

</style>
