<template>
  <div id="app">
    <todo-list :todos="todos" @new="pushTask" @remove="removeTask"></todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList'

export default {
  name: 'App',
  components: {
    TodoList
  },
  data () {
    return {
      todos: [
        {
          task: 'Task 1',
          time: '13:00',
          done: true
        },
        {
          task: 'Task 2',
          time: '15:00',
          done: false
        },
        {
          task: 'Task 3',
          time: '10:00',
          done: true
        }
      ]
    }
  },
  methods: {
    pushTask (text, time) {
      this.todos.push({task: text, time: time, done: false})
    },
    removeTask (index) {
      this.$delete(this.todos, index)
    }
  }
}
</script>

<style>
body{
  background: #757F9A;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to left, #D7DDE8, #757F9A);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to left, #D7DDE8, #757F9A); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
#app {
  display: flex;
}
</style>
