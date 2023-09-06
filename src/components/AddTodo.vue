<template>
  <form @submit="addItem" class="add-form">
    <input type="text" placeholder="Add new todo item..." v-model="title"/>
    <input type="submit" name="Add Todo Item" id="" />
  </form>
</template>

<script>
import {ref} from 'vue'
// import {v4 as uuid} from 'uuid' 
export default {
    name: 'FormAdd',
    setup(props, context) {
        const title = ref('')
        const addItem = event => {
            event.preventDefault()
            const newItem ={
                // id: uuid(),
                title: title.value,
                status: false
            }
            context.emit('add-item', newItem)
            title.value = ''
        }
        
        return {
            title,
            addItem
        }
    }
}
    
</script>

<style>
.add-form{
    display: flex;
    justify-content: space-between;
}
input[type=text]{
    width: 80%;
    padding: 10px
}
input[type=submit]{
    width: 15%;
}
</style>