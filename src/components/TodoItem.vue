<template>
    <div :class="['todo-item', todoProps.completed ? 'is-completed' : ''] ">
        <input type="checkbox" :checked="todoProps.completed" @change="markItemCompleted">
        <p>{{ todoProps.title }}</p>
        <button class="del-btn" @click="deleteItem">Delete</button>
    </div>
</template>

<script>

export default {
    name: 'TodoItem',
    props: ['todoProps'],
    setup(props, context) {
        const markItemCompleted = () => {
            context.emit('item-completed', props.todoProps.id)
        }

        const deleteItem = () => {
            context.emit('item-deleted', props.todoProps.id)
        }

        return  {
            markItemCompleted,
            deleteItem
        }
    }
}
</script>

<style>
    .todo-item {
        display: flex;
        background: #f4f4f4;
        padding: 10px;
        margin: 0;
        border-bottom: 1px solid #cccc;
    }

    .is-completed p {
        text-decoration: line-through;
    }

    .del-btn {
        background: #ff0000;
        color: #ffff;
        border: none;
        cursor: pointer;
        border: none;
    }
</style>