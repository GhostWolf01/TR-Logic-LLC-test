<template>
    <div class="todos-list" @click="clickTodoList($event)">
      <Todo v-for="(elem, index) in todolist"
      :key="index"
      :header="elem.header"
      :todoElems="elem.todoElems"></Todo>
    </div>
</template>

<script>
import Todo from './Todo.vue'

export default {
  name: 'TodoList',
  components: {
    Todo
  },
  props: {
    todolist: {
      type: Array,
      // eslint-disable-next-line vue/require-valid-default-prop
      default: []
    }
  },
  methods: {
    clickTodoList (event) {
      if (this.$el === event.target) {
        for (const el of this.$children) {
          el.active = false
        }
        this.$root.$children[0].activeIndex = -1
      }
    }
  }
}
</script>

<style lang="scss">
.todos-list{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: flex-start;
}
</style>
