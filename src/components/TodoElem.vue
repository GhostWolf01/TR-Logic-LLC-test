<template>
    <div class="todo-elem">
        <input class="todo-elem__checkbox" :value="valueCheck" :disabled="checkActive"  type="checkbox"><input class="todo-elem__text" :value="value" :readonly="readonly" type="text">
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
  }
}
</script>

<style lang="scss">
    .todo-elem{
        width: 100%;
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
        }
    }
</style>
