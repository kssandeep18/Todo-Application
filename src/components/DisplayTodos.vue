<template>
  <div>
    <div v-if="todos.length">
        <div v-for="todo in todos" :key=todo.id class="card-panel teal" :id=todo.id>
            <span class="white-text">{{todo.content}} </span>
            <i class="material-icons right" @click="deleteTodo">delete</i>
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
        todos: Array
    },
    methods: {
        deleteTodo: function(e) {
            this.$emit("deleteTodo",e.target.parentNode.id);
        }
    }
}
</script>

<style scoped>
.material-icons {
    cursor: pointer;
}
</style>
