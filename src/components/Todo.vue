<template>
    <div class="todo" :class="[{ 'todo--active' : active }, { 'todo--open' : todoOpen }, { 'todo--visible' : visible }]" @click="activeTodo()">
        <h2 class="todo__header">{{header}}</h2>
        <div class="todo__content">
            <TodoElem v-for="(elem, index) in todoElems"
                :key="index"
                :value="elem.value"
                :valueCheck="elem.valueCheck"
                :readonly="!writeText"
                :checkActive="!todoOpen">
            </TodoElem>
        </div>
    </div>
</template>

<script>
import TodoElem from './TodoElem.vue'

export default {
  name: 'Todo',
  components: {
    TodoElem
  },
  props: {
    header: {
      type: String,
      default: 'Название 1'
    },
    todoElems: {
      type: Array,
      // eslint-disable-next-line vue/require-valid-default-prop
      default: [
        {
          value: 'Задание 1',
          valueCheck: false
        }
      ]
    }
  },
  data () {
    return {
      active: false,
      todoOpen: false,
      visible: false,
      writeText: false
    }
  },
  methods: {
    activeTodo () {
      for (let i = 0; i < this.$parent.$children.length; i++) {
        this.$parent.$children[i].active = false
        if (this.$parent.$children[i]._uid === this._uid) {
          this.$root.$children[0].activeIndex = i
        }
      }
      this.active = true
    }
  }
}
</script>

<style lang="scss">
    .todo{
        display: flex;
        overflow: hidden;
        height: max-content;
        max-height: 100px;
        width: 20%;
        flex-direction: column;
        justify-content: start;
        align-items: center;
        padding: 10px 20px 20px 20px;
        border: 3px solid rgba($color: #ffc107, $alpha: 0.6);
        border-radius: 10px;
        background-color: rgba($color: #28a745, $alpha: 0.6) ;
        margin-top: 10px;
        &__header{
            font-family: 'Roboto';
            font-weight: normal;
            font-size: 28px;
            line-height: 28px;
            width: 100%;
            text-align: center;
            padding-bottom: 5px;
            margin-bottom: 5px;
            border-bottom: 1px solid #343a40;
        }
        &__content{
            display: flex;
            overflow: hidden;
            width: 100%;
            height: 100%;
            flex-direction: column;
            justify-content: start;
            align-items: center;
        }
        &--active{
            background-color: rgba($color: #28a745, $alpha: 1) ;
            border: 5px solid rgba($color: #ffc107, $alpha: 0.8);
        }
        &--open{
          width: 60%;
          max-height: max-content;
        }
        &--visible{
          display: none;
        }
    }
</style>
