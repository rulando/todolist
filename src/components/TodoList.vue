<template>
  <div class="todo-list">
    <div class="header">
      <h1>Todo List With Vuejs</h1>
      <div class="task-count">
        <h2>Completed Task: {{todos.filter(todo => {return todo.done === true}).length}} </h2>
        <h2>Pending Task: {{todos.filter(todo => {return todo.done === false}).length}} </h2>
      </div>
    </div>
    <div class="content">
      <div class="list" v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" class="list-item checkbox-styled" v-model="todo.done">
        <label class="list-item" :class="{ done: todo.done}">{{ todo.task }}</label>
        <label class="list-item">{{ todo.time }}</label>
        <label class="remove" @click="remove(index)">&times;</label>
      </div>
    </div>
    <div class="error" v-show="this.error">
      {{ this.error }}
    </div>
    <div class="composer">
      <input type="text" class="list-input" placeholder="Input Task Here.." v-model="text">
      <input type="time" class="list-input" v-model="time">
    </div>
    <input type="submit" class="list-input" value="DOIT" @click="newTask">
  </div>
</template>
<script>
export default{
  props: ['todos'],
  data () {
    return {
      text: null,
      time: null,
      done: false,
      error: null,
      modal: false
    }
  },
  methods: {
    newTask () {
      if (this.text == null && this.time == null) {
        this.error = 'Please Insert Task and Time Correctly'
      } else if (this.text != null && this.time == null) {
        this.error = 'Please Insert Time Correctly'
      } else if (this.text == null && this.time != null) {
        this.error = 'Please Insert Task Correctly'
      } else if (this.text != null && this.time != null) {
        this.$emit('new', this.text, this.time)
        this.error = ''
        this.text = null
        this.time = null
      }
    },
    remove (index) {
      this.$emit('remove', index)
    }
  }
}
</script>
<style>
  .todo-list{
    text-align: center;
    flex: 1 auto;
  }
  .header{
    color: #fff;
  }
  .task-count{
    display: flex;
    width: 500px;
    margin: auto;
  }
  .task-count h2{
    flex: 1;
    text-align: left;
  }
  .content{
    width: 500px;
    margin: auto;
    background-color: #f2f2f2;
    border-radius: 5px;
  }
  .list{
    display: flex;
    width: 500px;
    margin: auto;
    padding: 20px 0;
    color: #808080;
    border-bottom: 1px solid #b3b3b3;
  }
  .list-item{
    flex: 1;
    text-align: left;
    font-size: 1.5em;
    font-weight: lighter;
  }
  .remove{
    flex: 0.2;
    text-align: right;
    margin-right: 10px;
    font-size: 1.5em;
    cursor: pointer;
    font-weight: bolder;
  }
  input[type=checkbox]{
    transform: scale(1.5);
    margin: auto 0 auto -50px;
  }
  .error{
    margin: 20px auto 5px;
    color: #d8112c;
    font-size: 1.5em;
  }
  .composer{
    display: flex;
    width: 500px;
    margin: 20px auto 5px;
  }
  input[type=text]{
    flex: 2;
    height: 40px;
    width: 40px;
    font-size: 1.5em;
    color: #808080;
    border-radius: 5px 0 0 5px;
    padding: 0 10px;
    background-color: #f2f2f2;
    border: none;
    border-right: 1px solid #808080;
  }
  input[type=time]{
    flex: 1;
    height: 40px;
    width: 10px;
    font-size: 1.5em;
    color: #808080;
    background-color: #f2f2f2;
    border-radius: 0 5px 5px 0;
    border: none;
    cursor: pointer;
  }
  input[type=submit]{
    height: 40px;
    width: 500px;
    font-size: 1.5em;
    color: #808080;
    border-radius: 5px;
    background-color: #f2f2f2;
    border: none;
    cursor: pointer;
  }
  .done{
    text-decoration: line-through;
  }
</style>
