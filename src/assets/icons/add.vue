<template>
<div>
  <svg @click="addTodo()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48"><title>{{title}}</title>
      <g fill="#000000">
          <path d="M38 6H10c-2.21 0-4 1.79-4 4v28c0 2.21 1.79 4 4 4h28c2.21 0 4-1.79 4-4V10c0-2.21-1.79-4-4-4zm-4 20h-8v8h-4v-8h-8v-4h8v-8h4v8h8v4z"/>
      </g>
  </svg>
</div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'add'
    },
    todoOpen: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    addTodo () {
      if (!this.todoOpen) {
        const app = this.$root.$children[0]
        app.$children[app.$children.length - 1].todolist.push({
          header: 'Новий Заголовок',
          todoElems: [
            {
              value: 'Задание',
              valueCheck: false
            }
          ]
        })
        // Next Tick
        this.$nextTick(function () {
          const todolist = app.$children[app.$children.length - 1].$children
          for (let i = 0; i < todolist.length; i++) {
            todolist[i].active = false
            if (todolist[i]._uid === todolist[todolist.length - 1]._uid) {
              app.activeIndex = i
            }
          }
          todolist[todolist.length - 1].active = true
          app.$children[5].openTodo()
          this.$nextTick(function () {
            app.$children[5].openTodo()
          })
        })
      } else {
        const app = this.$root.$children[0]
        const todolist = app.$children[app.$children.length - 1]
        todolist.todolist[app.activeIndex].todoElems.push({
          value: 'Задание 1',
          valueCheck: false
        })
        app.$children[5].openTodo()
      }
    }
  }
}
</script>

<style lang="scss">
  svg{
    margin-right: 10px;
    cursor: pointer;
    &:hover{
      background-color: rgba($color: #343a40, $alpha: 0.4);
    }
  }
</style>
