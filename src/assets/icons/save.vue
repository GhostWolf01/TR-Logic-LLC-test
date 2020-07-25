<template>
<div>
  <svg @click="save()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48"><title>{{title}}</title>
  <g fill="#000000">
  <path d="M34 6H10c-2.21 0-4 1.79-4 4v28c0 2.21 1.79 4 4 4h28c2.21 0 4-1.79 4-4V14l-8-8zM24 38c-3.31 0-6-2.69-6-6s2.69-6 6-6 6 2.69 6 6-2.69 6-6 6zm6-20H10v-8h20v8z"/>
  </g>
  </svg>
  <div class="mesage" :class="{'mesage--open' : !mesageOpen}">
    <p class="mesage__text">Сохранено</p>
    <button class="mesage__btn" @click="mesageOk()">OK</button>
  </div>
</div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'save'
    }
  },
  data () {
    return {
      mesageOpen: false
    }
  },
  methods: {
    save () {
      const app = this.$root.$children[0]
      const todolist = app.$children[app.$children.length - 1]
      for (let i = 0; i < todolist.$children.length; i++) {
        todolist.todolist[i].header = todolist.$children[i].header
        todolist.todolist[i].todoElems = todolist.$children[i].todoElems
      }
      app.todolist = todolist.todolist
      localStorage.TodoList = JSON.stringify(app.todolist)
      this.mesageOpen = true
    },
    mesageOk () {
      this.mesageOpen = false
    }
  }
}
</script>

<style lang="scss">
  .mesage{
    position: absolute;
    top: 25%;
    left: 35%;
    height: 25%;
    width: 25%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 10px 20px 20px 20px;
    background-color: rgba($color: #28a745, $alpha: 1) ;
    border: 5px solid rgba($color: #ffc107, $alpha: 0.8);
    border-radius: 15px;
    &__text{
      width: 100%;
      font-family: Roboto;
      font-size: 28px;
      line-height: 28px;
      text-align: center;
      margin-bottom: 20px;
    }
    &__btn{
      cursor: pointer;
      font-family: Roboto;
      font-size: 28px;
      line-height: 28px;
      text-align: center;
      padding: 5px;
      width: 60%;
      height: 40px;
      background-color: rgba($color: #28a745, $alpha: 1) ;
      border: 3px solid rgba($color: #ffc107, $alpha: 0.8);
      &:hover{
        background-color: rgba($color: #343a40, $alpha: 0.7) ;
      }
    }
    &--open{
      display: none;
    }
    @media screen and (max-width: 768px) {
      height: 25%;
      width:  60%;
      left: 14%;
    }
  }
</style>
