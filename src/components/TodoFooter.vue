<template>
  <footer class="footer" v-if="list.length > 0">
    <!-- This should be `0 items left` by default -->
    <span class="todo-count"
      ><strong>{{ leftNum }}</strong> item left</span
    >
    <!-- Remove this if you don't implement routing -->
    <ul class="filters">
      <li>
        <a
          :class="{ selected: this.type === 'all' }"
          @click.prevent="changeType('all')"
          href="#/"
          >All</a
        >
      </li>
      <li>
        <a
          href="#/active"
          :class="{ selected: this.type === 'active' }"
          @click.prevent="changeType('active')"
          >Active</a
        >
      </li>
      <li>
        <a
          href="#/completed"
          :class="{ selected: this.type === 'completed' }"
          @click.prevent="changeType('completed')"
          >Completed</a
        >
      </li>
    </ul>
    <!-- Hidden if no completed items are left ↓ -->
    <button class="clear-completed" v-show="isShow" @click="clear">
      Clear completed
    </button>
  </footer>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      require: true,
    },
    type: {
      type: String,
      default: 'all',
    },
  },
  computed: {
    leftNum() {
      const obj = this.list.filter((item) => {
        return !item.isDone
      })
      return obj.length
    },
    isShow() {
      const obj = this.list.filter((item) => {
        return item.isDone
      })
      return obj.length > 0
    },
  },
  methods: {
    clear() {
      this.$emit('clear')
    },
    changeType(theType) {
      this.$emit('changeType', theType)
    },
  },
}
</script>

<style></style>
