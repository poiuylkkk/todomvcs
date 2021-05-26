<template>
  <div>
    <section class="todoapp">
      <TodoHeader @add="addFn"></TodoHeader>
      <TodoMain
        :list="showList"
        @del="delFn"
        @change="changeFn"
        @yesEdit="yesFn"
        :type="type"
        @total="totalFn"
      ></TodoMain>
      <TodoFooter
        :list="list"
        :type="type"
        @clear="clearFn"
        @changeType="changeTypeFn"
      ></TodoFooter>
    </section>
    <footer class="info">
      <p>Double-click to edit a todo</p>
      <!-- Remove the below line ↓ -->
      <p>Template by <a href="http://sindresorhus.com">黑马</a></p>
      <!-- Change this out with your name and url ↓ -->
      <p>Created by <a href="http://todomvc.com">陈俊宏</a></p>
      <p>Part of <a href="http://todomvc.com">TodoMVC</a></p>
    </footer>
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter'
import TodoHeader from './components/TodoHeader'
import TodoMain from './components/TodoMain'
export default {
  data() {
    return {
      // list: [
      //   {
      //     id: 1,
      //     title: '吃饭',
      //     isDone: false,
      //   },
      //   {
      //     id: 2,
      //     title: '睡觉',
      //     isDone: true,
      //   },
      //   {
      //     id: 3,
      //     title: '打豆豆',
      //     isDone: true,
      //   },
      // ],
      list: JSON.parse(localStorage.getItem('todoMVC')) || [],
      type: 'all',
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    delFn(id) {
      this.list = this.list.filter((item) => {
        return item.id !== id
      })
    },
    changeFn(id) {
      const obj = this.list.find((item) => {
        return item.id === id
      })
      obj.isDone = !obj.isDone
    },
    addFn(name) {
      this.list.unshift({
        id: Date.now(),
        title: name,
        isDone: false,
        date: new Date(),
      })
    },
    yesFn(id, title) {
      console.log(id, title)
      const obj = this.list.find((item) => {
        return item.id === id
      })
      obj.title = title
    },
    clearFn() {
      this.list = this.list.filter((item) => {
        return !item.isDone
      })
    },
    changeTypeFn(theType) {
      this.type = theType
    },
    totalFn(theTotal) {
      return this.list.forEach((item) => (item.isDone = theTotal))
    },
  },
  computed: {
    showList() {
      if (this.type === 'active') {
        return this.list.filter((item) => !item.isDone)
      } else if (this.type === 'completed') {
        return this.list.filter((item) => item.isDone)
      } else {
        return this.list
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(value) {
        localStorage.setItem('todoMVC', JSON.stringify(value))
      },
    },
  },
}
</script>

<style></style>
