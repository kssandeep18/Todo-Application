<template>
    <div class="row">
        <form action="">
            <div class="input-field col s12">
                <input id="todo" type="text" class="validate" v-model="newTodo" @keypress.enter.prevent="addTodo" required />
                <label for="todo">Todo</label>
            </div>
            <span class="red-text" :class="{hide:!isSame}">Todo already exists!</span>
        </form>
    </div>
</template>

<script>
export default {
    props: {
        todos: Array
    },
    data() {
        return {
            newTodo:""
        }
    },
    methods: {
        addTodo: function(e) {
            if(this.newTodo.length===0 || this.newTodo.trim().length===0 || this.isSame) {
                return false;
            }
           this.$emit("addTodo",this.newTodo);
           this.newTodo="";
        }
    },
    computed: {
        isSame(){
            let result = this.todos.find(each =>{
                if(each.content === this.newTodo){
                    return true;
                }
                return false;
            })
            if(result){
                return true
            }
            return false;
            for(var todo of this.todos) {
                if(todo.content===this.newTodo) {
                    return true;
                }
            }  
            return false;  
        }
    }
    /*watch: {
        newTodo: function(newVal) {
            this.isSame=false;        
            this.todos.forEach(todo => {
                if(todo.content===newVal) {
                    console.log(todo.content +"  "+ newVal);
                    this.isSame=true;
                    flag++;
                }
            });
        }
    }*/
}
</script>

<style scoped>
    .hide {
        display: none;
    }
</style>
