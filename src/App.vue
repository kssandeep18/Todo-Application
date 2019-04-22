<template>
  <div id="app" class="container">
    <h1 class="center">Todo App</h1><br/>
    <display-todos :todos=todos @deleteTodo="deleteTodo($event)" @toggleTodo="toggleTodo($event)" :completedCount="completedCount" :pendingCount="pendingCount"></display-todos>
    <add-todo @addTodo="addTodo($event)" :todos="todos"></add-todo>
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
        {id:1, content:"To drink water", isCompleted:false},
        {id:2, content:"To complete assignment", isCompleted:false}
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
      let todosAfterInsertion=[...this.todos,{id:newId, content:newTodo, isCompleted:false}];
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
    },
    toggleTodo: function(id) {
      let targetId=this.todos.findIndex(todo=>todo.id==id);
      this.todos[targetId].isCompleted=!this.todos[targetId].isCompleted;
    }
  },
  computed: {
    completedCount(){
      let completedCount = 0;
      this.todos.forEach(todo => {
        if(todo.isCompleted == true)
          completedCount++;
      });
      return completedCount;
    },
    pendingCount(){
      let pendingCount = 0;
      this.todos.forEach(todo => {
        if(todo.isCompleted !== true)
          pendingCount++;
      });
      return pendingCount;
    }
  }
}
</script>

<style>

</style>
