<template>
<div>
  <svg @click="clickDelete()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48"><title>trash-simple</title><g stroke-linecap="square" stroke-linejoin="miter" stroke-width="2" fill="#000000" stroke="#000000"><polyline fill="none" stroke="#000000" stroke-miterlimit="10" points="40,16 40,46 8,46 8,16 "></polyline> <line fill="none" stroke="#000000" stroke-miterlimit="10" x1="2" y1="10" x2="46" y2="10"></line> <line fill="none" stroke-miterlimit="10" x1="24" y1="22" x2="24" y2="37"></line> <line fill="none" stroke-miterlimit="10" x1="16" y1="22" x2="16" y2="37"></line> <line fill="none" stroke-miterlimit="10" x1="32" y1="22" x2="32" y2="37"></line> <polyline fill="none" stroke="#000000" stroke-miterlimit="10" points="16,10 16,2 32,2 32,10 "></polyline></g>
  </svg>
  <div class="mesage" :class="{'mesage--open' : !mesageOpen}">
    <p class="mesage__text">{{text}}</p>
    <div class="mesage__btns">
      <button class="mesage__btn" @click="deleteTodo()">Да</button>
      <button class="mesage__btn" @click="clickNo()">Нет</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'trash simple'
    },
    todoOpen: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      mesageOpen: false,
      text: ''
    }
  },
  methods: {
    clickDelete () {
      this.mesageOpen = true
      const app = this.$root.$children[0]
      if (this.todoOpen) {
        this.text = 'Удалить выбраную строку?'
        const todolist = app.$children[app.$children.length - 1]
        const todo = todolist.$children[app.activeIndex]
        if (todo.activeElem === -1) {
          this.text = 'Удалить выбраную заметку?'
        }
      } else {
        this.text = 'Удалить выбраную заметку?'
        if (app.activeIndex === -1) {
          this.text = 'Выбирите заметку!'
        }
      }
    },
    clickNo () {
      this.mesageOpen = false
    },
    deleteTodo () {
      const app = this.$root.$children[0]
      const todolist = app.$children[app.$children.length - 1]
      if (this.todoOpen) {
        const todo = todolist.$children[app.activeIndex]
        if (todo.activeElem > -1) {
          todo.todoElems.splice(todo.activeElem, 1)
          for (const el of todo.$children) {
            el.active = false
          }
          todo.activeElem = -1
        } else {
          todolist.todolist.splice(app.activeIndex, 1)
          for (const el of todolist.$children) {
            el.active = false
          }
          app.activeIndex = -1
          app.$children[0].back()
        }
      } else {
        if (app.activeIndex > -1) {
          todolist.todolist.splice(app.activeIndex, 1)
          for (const el of todolist.$children) {
            el.active = false
          }
          app.activeIndex = -1
        }
      }
      this.mesageOpen = false
    }
  }
}
</script>

<style lang="scss" scoped>
.mesage{
  &__btns{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    align-items: center;
    width: 100%;
  }
  &__btn{
    width: 45%;
  }
}
</style>
