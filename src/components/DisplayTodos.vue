<template>
  <div>
    <div v-if="todos.length">
        <h5>Completed:{{completedCount}}  Pending: {{pendingCount}}</h5> 
        <div v-for="todo in todos" :key="todo.id" class="card-panel teal" :id="todo.id">
            <span class="white-text">{{todo.content}} </span>
            <i class="material-icons right" v-show="!todo.isCompleted" @click="toggle(todo.id)">report</i>
            <i class="material-icons right" v-show="todo.isCompleted" @click="toggle(todo.id)">playlist_add_check</i>
            <i class="material-icons right" @click="deleteTodo(todo.id)">delete</i>
        </div>
    </div>
    <div v-else>
        <h4>Add your First Todo!</h4>
    </div>

  </div>
</template>

<script>

export default {
    name: 'DisplayTodos',
    props: {
        todos: Array,
        completedCount: Number,
        pendingCount: Number
    },
    data() {
        return {
        }
    },
    methods: {
        deleteTodo: function(id) {
            this.$emit("deleteTodo",id);
        },
        toggle: function(id) {
            this.$emit("toggleTodo",id);
        }
    }
}
</script>

<style scoped>
.material-icons {
    cursor: pointer;
}
</style>
