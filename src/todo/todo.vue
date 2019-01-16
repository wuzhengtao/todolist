<template>
    <section class="real-app">
        <input 
            type="text"
            class="add-input"
            autofocus="autofocus"
            placeholder="添加一个代办事项"
            @keyup.enter="addTodo"
        >
        <item 
            :todo="todo"
            v-for="todo in todos"
            :key="todo.id"
            @del = "deleteTodo"
        />
        <tabs 
            :filter="filter" 
            :todos="todos" 
            @toggle = "toggleFilter"
        />
    </section>
</template>

<script>
import '../assets/styles/todo.styl'
import Item from './item.vue'
import Tabs from './tabs.vue'

let id = 0

export default {
    data () {
        return {
            todos: [],
            filter: 'all'
        }
    },
    components: {
        Item, Tabs,
    },
    methods: {
        addTodo(e) {
            this.todos.unshift({
                id: id++,
                content: e.target.value.trim(),
                completed: false
            })
            e.target.value = ''
        },
        deleteTodo(id) {
            this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
        },
        toggleFilter(state) {
            this.filter = state
        }
    }
};
</script>

