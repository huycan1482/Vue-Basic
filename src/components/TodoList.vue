<template>
    <div>
        <AddTodo @add-todo="addTodo"/>

        <TodoItem 
        v-for="todo in todos" 
        :key="todo.id" 
        :todoProps="todo"
        @item-completed="markCompleted"
        @item-deleted="deleteTodo"
        />

        <!-- <TodoItem 
        v-for="todo in todos" 
        v-bind:key="todo.id" 
        v-bind:todoProps="todo"
        v-on:item-completed="markCompleted"/> -->
    </div>

</template>

<script>
import { ref } from 'vue'
import TodoItem from './TodoItem'
import AddTodo from './AddTodo'
import axios from 'axios'

export default {
    name: 'TodoList',
    components: { TodoItem, AddTodo },
    setup() {
        const todos = ref([])

        const getAllTodos = async () => {
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
                todos.value = res.data
            } catch (e) {
                console.log(e.message)
            }
        }
        getAllTodos()
        const markCompleted = id => {
            todos.value = todos.value.map(todo => {
                if (todo.id === id) todo.completed = !todo.completed;
                return todo;
            });
        }

        const deleteTodo = async id => {
            try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !== id);
            } catch (e) {
                console.log(e.message)
            }
        }
        
        const addTodo = async newTodo => {
            try {
                const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newTodo)
                todos.value.push(res.data)
            } catch (e) {
                console.log(e.message)
            }
        }
        return  {
            todos,
            markCompleted,
            deleteTodo,
            addTodo
        }
    }
}
</script>

<style>

</style>