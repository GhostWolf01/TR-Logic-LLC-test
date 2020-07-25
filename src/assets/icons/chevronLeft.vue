<template>
<div>
  <svg @click="clickBack()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48"><title>{{title}}</title>
      <g fill="#000000">
          <path d="M30.83 14.83L28 12 16 24l12 12 2.83-2.83L21.66 24z"/>
      </g>
  </svg>
  <div class="mesage" :class="{'mesage--open' : !mesageOpen}">
    <p class="mesage__text">Сохранить изменения?</p>
    <div class="mesage__btns">
      <button class="mesage__btn" @click="save()">Да</button>
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
      default: 'chevron left'
    }
  },
  data () {
    return {
      mesageOpen: false
    }
  },
  methods: {
    save () {
      this.$root.$children[0].$children[3].save()
      this.back()
      this.mesageOpen = false
    },
    clickNo () {
      const app = this.$root.$children[0]
      if (localStorage.TodoList !== '') {
        app.todolist = JSON.parse(localStorage.TodoList)
      } else {
        app.todolist = []
      }
      this.back()
      this.mesageOpen = false
    },
    clickBack () {
      this.mesageOpen = true
    },
    back () {
      const app = this.$root.$children[0]
      const todolist = app.$children[app.$children.length - 1]
      for (const el of todolist.$children) {
        for (const elem of el.$children) {
          elem.active = false
        }
        el.active = false
        el.visible = false
        el.todoOpen = false
        el.writeText = false
        el.activeElem = -1
      }
      app.activeIndex = -1
      app.todoOpen = false
    }
  }
}
</script>

<style lang="scss" scoped>
svg{
  border: 2px solid rgba($color: #ffc107, $alpha: 0.6);
  border-radius: 50%;
}
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
