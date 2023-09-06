<template>
    <AddTodo  @add-item="addNew"></AddTodo>
    <div class="todo-list">
        <TodoItem 
            v-for="todo in todos" 
            :key="todo.id" 
            :toProps="todo"
            @item-checked="markCompleted"
            @delete-item="deleteTodo"
        >{{ todo }}
        </TodoItem>
    </div>
</template>
<script>
import { ref } from 'vue'
// import { v4 as uuid } from 'uuid'
import axios from 'axios'

import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
export default {
    name: 'TodoList',
    components: { TodoItem, AddTodo },

    setup() {
        const todos = ref([])
        const getAllTodo = async () => {
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
                todos.value = res.data
            } catch (error) {
                console.log(error)
            }
        }
        getAllTodo()
        const markCompleted = id => {
            console.log(id)
            todos.value = todos.value.map(todo =>{
                if (todo.id === id) todo.status = !todo.status;
                return todo
            })
        }
        const deleteTodo = async id => {
            try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !== id)

            } catch (error) {
                console.log(error)
            }
        }
        const addNew = async item =>{
            try {
                const res = await axios.post('https://jsonplaceholder.typicode.com/todos', item)
                todos.value.push(res.data)
                // todos.value.push()
            } catch (error) {
                console.log(error)
            }
        }
        return {
            todos,
            markCompleted,    
            deleteTodo,   
            addNew
        }
    }
}
</script>

<style>

</style>