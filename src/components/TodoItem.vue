<template>
  <p :class="['todo-item', toProps.status ? 'completed' : '']" :id="toProps.id">
    <input type="checkbox" :checked="toProps.status" @change="itemChecked">
    <span>{{ toProps.title }}</span>
    <button class="delete-item" @click="deleteItem">Delete</button></p>
</template>

<script>
export default {
    name: 'TodoItem',
    props: ['toProps'],
    setup(props, context) {
        const itemChecked = () => {
            context.emit('item-checked', props.toProps.id)
        }
        const deleteItem = () => {
            context.emit('delete-item', props.toProps.id)
        }
        return {
        itemChecked,
        deleteItem
        }
    }
    
}
</script>

<style>
.todo-item{
    color: blue;
    font-size: 16px;
    display: flex;
    align-items:center;

}
.delete-item{
    background-color: #000;
    color: #fff;
    border-radius: 0;
    margin-left: 10px;
    padding: 5px;
    margin-left: auto;
    cursor: pointer;
}
input[type=checkbox]{
    cursor: pointer;
}
.todo-item.completed span{
    text-decoration: line-through;
}
</style>