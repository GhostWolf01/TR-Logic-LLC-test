<template>
  <svg @click="deleteTodo()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48"><title>trash-simple</title><g stroke-linecap="square" stroke-linejoin="miter" stroke-width="2" fill="#000000" stroke="#000000"><polyline fill="none" stroke="#000000" stroke-miterlimit="10" points="40,16 40,46 8,46 8,16 "></polyline> <line fill="none" stroke="#000000" stroke-miterlimit="10" x1="2" y1="10" x2="46" y2="10"></line> <line fill="none" stroke-miterlimit="10" x1="24" y1="22" x2="24" y2="37"></line> <line fill="none" stroke-miterlimit="10" x1="16" y1="22" x2="16" y2="37"></line> <line fill="none" stroke-miterlimit="10" x1="32" y1="22" x2="32" y2="37"></line> <polyline fill="none" stroke="#000000" stroke-miterlimit="10" points="16,10 16,2 32,2 32,10 "></polyline></g>
  </svg>
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
          const app = this.$root.$children[0].$children
          for (const el of app[app.length - 1].$children) {
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

</style>
