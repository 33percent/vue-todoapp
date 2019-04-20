<template>
    <div>
        <form @submit="addTodo">
            <input type='text' v-model='title' name='title' placeholder="add todo..."/>
            <input type='submit' value='add todo' class="btn"/> 
        </form>
    </div>
</template>
<script>
export default {
    name:'AddTodo',
    data() {
        return {
            title:''
        }
    },
    methods:{
        addTodo(e) {
            const newTodo = {
                title:this.title,
                completed:false,
            }
            // emit to parent
            this.$emit('add-todo',newTodo);
            this.title = '';
        e.preventDefault();
        }
    }
}
</script>
<style scoped>
form {
    display: flex;
}
input[type='text'] {
    flex: 10;
    padding: 5px;
}
input[type='submit'] {
    flex:2
}
</style>
