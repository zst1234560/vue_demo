<template>
  <li
    :class="{'high-light':isEnter}"
    @mouseenter="isEnter = true"
    @mouseleave="isEnter = false"
  >
    <label>
      <input
        type="checkbox"
        :checked='todo.done'
        @change='updateTodo(index,$event)'
      />
      <span v-show="!todo.isEdit">{{todo.name}}</span>
      <input
        type="text"
        v-show="todo.isEdit"
        v-model="todo.name"
        @blur="updateEdit(index,$event)"
        ref="editTodoIpt"
      >
    </label>
    <button
      class="btn btn-danger"
      :style="{display: isEnter ? 'block' : 'none'}"
      @click="deleteT()"
    >删除</button>
    <button
      class="btn btn-edit"
      :style="{display: isEnter ? 'block' : 'none'}"
      @click="editTodo(todo)"
    >编辑</button>
  </li>
</template>

<script>
export default {
    props: ['todo','index','updatedTodos','deleteTodo'],
    data() {
        return {
            isEnter: false
        }
    },
    methods: {
        updateTodo(index, event) {
            this.updatedTodos(index,event.target.checked)
        },
        updateEdit(index,event) {
          if (event.target.value == '') return alert('输入内容不能为空')
          this.todo.isEdit = false
          this.updatedTodo(index,event.target.value)
        },
        deleteT() {
          if(confirm('确认删除吗')) {
            this.deleteTodo(this.todo.id)
          }
        },
        editTodo(todo) {
          this.$set(todo,'isEdit',true)
          this.$nextTick(function() {
            this.$refs.editTodoIpt.focus()
          })
        }
    }
}
</script>

<style>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
.high-light {
  background-color: #ddd;
}
</style>