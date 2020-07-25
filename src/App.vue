<template>
  <div id="app">
    <header class="header">
        <chevronLeft title="Назад"></chevronLeft>
        <h1 class="header__text">Заметки</h1>
        <div class="header__controls">
          <rotateLeft title="Отменить"></rotateLeft>
          <rotateRight title="Повторить"></rotateRight>
          <save title="Сохранить"></save>
          <add title="Добавить" :todoOpen="todoOpen" ></add>
          <pencil title="Изменить" :todoOpen="todoOpen"></pencil>
          <trashSimple title="Удалить" :todoOpen="todoOpen"></trashSimple>
        </div>
    </header>
    <TodoList :todolist="todolist"></TodoList>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import chevronLeft from './assets/icons/chevronLeft.vue'
import rotateLeft from './assets/icons/rotateLeft.vue'
import rotateRight from './assets/icons/rotateRight.vue'
import save from './assets/icons/save.vue'
import trashSimple from './assets/icons/trash-simple.vue'
import pencil from './assets/icons/pencil.vue'
import add from './assets/icons/add.vue'

export default {
  name: 'App',
  components: {
    TodoList, trashSimple, pencil, add, chevronLeft, rotateRight, rotateLeft, save
  },
  data () {
    return {
      activeIndex: -1,
      todoOpen: false,
      todolist: [],
      todolistChange: [],
      todolistChangeActive: true
    }
  },
  watch: {
    todolist: {
      handler: function (val) {
        if (this.todolistChangeActive) {
          this.todolistChange.push(JSON.parse(JSON.stringify(val)))
          this.$children[1].indexChange = -1
          if (this.todolistChange.length > 100) {
            this.todolistChange.shift()
          }
          console.log(this.todolistChange)
        }
      },
      deep: true
    }
  },
  mounted () {
    if ((localStorage.TodoList != null) && (localStorage.TodoList !== '')) {
      this.todolist = JSON.parse(localStorage.TodoList)
    }
    window.onbeforeunload = () => {
      this.$children[3].save()
      return false
    }
  },
  beforeDestroy () {
    this.$children[3].save()
  }
}
</script>

<style lang="scss">

@font-face {
  font-family: 'Roboto';
  src: url("./assets/fonts/Roboto-Medium.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}
@font-face {
  font-family: 'Roboto';
  src: url("./assets/fonts/Roboto-Regular.ttf") format("truetype");
  font-weight: 400;
  font-style: normal;
}
@font-face {
  font-family: 'Roboto';
  src: url("./assets/fonts/Roboto-Bold.ttf") format("truetype");
  font-weight: bold;
  font-style: normal;
}
*{
  margin: 0;
  padding: 0;
}
#app {
  height: 100%;
}
.header{
  width: 100%;
  box-sizing: border-box;
  height: 60px;
  padding: 10px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: rgba($color: #28a745, $alpha: 0.7) ;
  &__text{
    font-family: 'Roboto';
    font-size: 48px;
    line-height: 48px;
    color: black;
  }
  &__controls{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  @media screen and (max-width: 768px) {
    justify-content: center;
    flex-wrap: wrap;
    height: max-content;
  }
}

</style>
