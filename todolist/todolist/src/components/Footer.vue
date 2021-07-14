<template>
  <div class="todo-footer" v-show="Total">
        <label>
          <input type="checkbox" v-model="isAll"/>
        </label>
        <span>
          <span>已完成{{doneTodo}}</span> / {{Total}}
        </span>
        <button class="btn btn-danger" @click="remove">清除已完成任务</button>
      </div>
</template>

<script>
export default {
    name: 'Footer',
    props: ['todos','checkAllTodo','removeTodo'],
    computed: {
      doneTodo() {
        return this.todos.reduce( (pre,current) => pre += current.done ? 1 : 0, 0)
      },
      Total() {
        return this.todos.length
      },
      isAll: {
        set(e) {
          this.$emit('checkAllTodo',e)
        },
        get() {
          return this.Total == this.doneTodo && this.Total > 0
        }
      }
    },
    methods: {
      remove() {
        if(confirm('确定删除吗')) {
          this.$emit('removeTodo')
        }
      }
    }
}
</script>

<style scoped>
/*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>