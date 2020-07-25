<template>
    <div class="todo-elem" :class="{ 'todo-elem--active' : active}" @click="activeElem()">
        <input class="todo-elem__checkbox" :disabled="checkActive" v-model="valueCheck" type="checkbox" @change="change()"><input class="todo-elem__text" :class="{ 'todo-elem__text--dec' : valueCheck}" @input="input()" v-model="value" :readonly="readonly" type="text">
    </div>
</template>

<script>
export default {
  name: 'TodoElem',
  props: {
    value: {
      type: String,
      default: ''
    },
    readonly: {
      type: Boolean,
      default: true
    },
    checkActive: {
      type: Boolean,
      default: true
    },
    valueCheck: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      active: false
    }
  },
  methods: {
    activeElem () {
      if (!this.checkActive) {
        for (let i = 0; i < this.$parent.$children.length; i++) {
          this.$parent.$children[i].active = false
          if (this.$parent.$children[i]._uid === this._uid) {
            this.$parent.activeElem = i
          }
        }
        this.active = true
      }
    },
    input () {
      this.$parent.todoElems[this.$parent.activeElem].value = this.value
    },
    change () {
      this.$parent.todoElems[this.$parent.activeElem].valueCheck = this.valueCheck
    }
  }
}
</script>

<style lang="scss">
.todo-elem{
  width: 99%;
  display: flex;
  justify-content: start;
  align-items: center;
  &__checkbox{
    width: 10%;
    height: 20px;
  }
  &__text{
    width: 90%;
    font-family: 'Roboto';
    font-size: 22px;
    border: none;
    background: none;
    &:focus{
      outline: none;
    }
    &--dec{
      text-decoration: line-through;
    }
  }
  &--active{
    background-color: rgba($color: #28a745, $alpha: 1) ;
    border: 3px solid rgba($color: #ffc107, $alpha: 0.8);
    border-radius: 25px;
  }
}
</style>
