<template>
    <div class="helper">
        <span class="left">{{unFinishedTodoLength}} items left</span>
        <span class="tabs">
            <span
                v-for="state in states"
                :key="state"
                :class="[state, filter === state ? 'actived' : '']"
                @click="toggleFilter(state)">
                {{state}}
            </span>
        </span>
        <span class="clear" @click="clearAllCompleted">Clear completed</span>
    </div>
</template>

<script>
import '../assets/styles/tabs.styl'
export default {
    props: {
        filter: {
            type: String,
            required: true,
        },
        todos: {
            type: Array,
            required: true
        }
    },
    computed: {
        unFinishedTodoLength() {
            return this.todos.filter(todo => !todo.completed).length
        }
    },
    methods: {
        toggltFilter() {
            this.$emit('toggle', state)
        },
        clearAllCompleted() {}
    },
    data() {
        return {
            states: ['all', 'active', 'completed']
        }
    }
}
</script>
