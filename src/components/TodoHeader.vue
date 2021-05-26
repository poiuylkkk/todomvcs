<template>
  <header class="header">
    <h1>todos</h1>
    <input
      class="new-todo"
      placeholder="What needs to be done?"
      autofocus
      @keyup.enter="add"
      v-model="name"
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      name: '',
    }
  },
  methods: {
    add() {
      if (this.name.trim() === '') {
        this.name = ''
        return alert('请输入任务信息！')
      }
      this.$emit('add', this.name)
      this.name = ''
    },
  },
}
</script>

<style></style>
