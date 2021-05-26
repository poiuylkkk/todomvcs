<template>
  <section class="main">
    <input id="toggle-all" class="toggle-all" type="checkbox" />
    <label for="toggle-all" @click="total">Mark all as complete</label>
    <ul class="todo-list">
      <!-- These are here just to show the structure of the list items -->
      <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
      <li
        :class="{ completed: item.isDone, editing: item.id === editId }"
        v-for="item in list"
        :key="item.id"
        @keyup.enter="yesEdit"
        @keyup.esc="noEdit"
      >
        <div class="view">
          <input
            class="toggle"
            type="checkbox"
            :checked="item.isDone"
            @change="change(item.id)"
          />
          <label @dblclick="edit(item.id, item.title)">{{ item.title }}</label>
          <button class="destroy" @click="del(item.id)"></button>
        </div>
        <input class="edit" v-model="editName" />
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: {
    list: {
      require: true,
      type: Array,
    },
    type: {
      type: String,
      default: 'all',
    },
  },
  methods: {
    del(id) {
      this.$emit('del', id)
    },
    change(id) {
      // console.log(id, '改变了')
      this.$emit('change', id)
    },
    edit(id, name) {
      console.log('编辑中')
      this.editId = id
      this.editName = name
    },
    yesEdit() {
      console.log('编辑完了')
      this.$emit('yesEdit', this.editId, this.editName)
      this.editId = ''
      this.editName = ''
    },
    noEdit() {
      this.editId = ''
      this.editName = ''
    },
    total() {
      console.log(222)
      this.theTotal = !this.theTotal
      this.$emit('total', this.theTotal)
    },
  },
  data() {
    return {
      editId: '',
      editName: '',
      theTotal: false,
    }
  },
}
</script>

<style></style>
