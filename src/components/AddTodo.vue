<template>
    <div class="row">
        <form>
            <div class="input-field col s12">
                <input id="todo" type="text" class="validate" v-model="newTodo" @keypress.enter.prevent="addTodo" required />
                <label for="todo">Todo</label>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newTodo:""
        }
    },
    methods: {
        addTodo: function(e) {
            if(this.newTodo.length===0) {
                return false;
            }
           this.$emit("addTodo",this.newTodo);
           e.target.parentNode.parentNode.reset();
        }
    }
}
</script>

<style

</style>
