<template>
  <svg @click="deleteTodo()" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 32 32" xml:space="preserve" width="32" height="32"><title>{{title}}</title><g stroke-linecap="square" stroke-linejoin="miter" stroke-width="2" fill="#111111" stroke="#111111"><polyline fill="none" stroke="#111111" stroke-miterlimit="10" points="27,10 27,31 5,31 5,10 "/> <line fill="none" stroke-miterlimit="10" x1="16" y1="15" x2="16" y2="25"/> <line fill="none" stroke-miterlimit="10" x1="11" y1="15" x2="11" y2="25"/> <line fill="none" stroke-miterlimit="10" x1="21" y1="15" x2="21" y2="25"/> <polyline fill="none" stroke="#111111" stroke-miterlimit="10" points="11,6 11,1 21,1 21,6 "/> <line fill="none" stroke="#111111" stroke-miterlimit="10" x1="30" y1="6" x2="2" y2="6"/></g></svg>
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
  methods: {
    deleteTodo () {
      if (this.todoOpen) {
        console.log()
      } else {
        if (this.$parent.activeIndex > -1) {
          this.$parent.todolist.splice(this.$parent.activeIndex, 1)
          for (const el of this.$root.$children[0].$children[3].$children) {
            el.active = false
          }
          this.$parent.activeIndex = -1
        }
      }
    }
  }
}
</script>

<style lang="scss">
  svg{
    cursor: pointer;
  }
</style>
