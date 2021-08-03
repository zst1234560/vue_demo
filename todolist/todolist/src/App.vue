<template>
    <div class="todo-container">
    <div class="todo-wrap">
      <!-- 头部 -->
      <Header @addObj='addObj'/>
      <!-- 列表 -->
      <List :todos='todos' :updatedTodos='updatedTodos' :deleteTodo='deleteTodo'/>
      <!-- 尾部 -->
      <Footer :todos='todos' @checkAllTodo='checkAllTodo' @removeTodo='removeTodo'/>
    </div>
  </div>
</template>

<script>
import Header from './components/Header'
import List from './components/List'
import Footer from './components/Footer'
export default {
  name: 'App',
  components: {Header,List,Footer},
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')) || []
    }
  },
  methods: {
    addObj(nameObj) {
      this.todos.unshift(nameObj)
    },
    updatedTodos(index, value) {
      this.todos[index].done = value
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    checkAllTodo(check) {
      this.todos.forEach(todo => todo.done = check)
    },
    removeTodo() {
      this.todos = this.todos.filter( todo => !todo.done)
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos',JSON.stringify(value))
      }
    }
  }
}
</script>

<style>
  /*base*/
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }
  .btn-edit {
    color: #fff;
    background-color: skyblue;
    border: 1px solid rgb(79, 149, 177);
    margin-right: 5px;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
  
</style>
