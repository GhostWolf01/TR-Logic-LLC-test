<template>
<div>
  <svg @click="openTodo()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48"><title>pencil</title><g stroke-linecap="square" stroke-linejoin="miter" stroke-width="2" fill="#000000" stroke="#000000"><line fill="none" stroke-miterlimit="10" x1="6" y1="32" x2="16" y2="42" stroke-linecap="butt"></line> <line fill="none" stroke-miterlimit="10" x1="11" y1="37" x2="31" y2="17" stroke-linecap="butt"></line> <line fill="none" stroke-miterlimit="10" x1="30" y1="8" x2="40" y2="18"></line> <line fill="none" stroke-miterlimit="10" x1="26" y1="12" x2="36" y2="22"></line> <path fill="none" stroke="#000000" stroke-miterlimit="10" d="M16,42L4,44l2-12L33.2,4.8 c1.6-1.6,4.1-1.6,5.7,0l4.3,4.3c1.6,1.6,1.6,4.1,0,5.7L16,42z"></path></g>
  </svg>
</div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'pencil'
    },
    todoOpen: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    openTodo () {
      if (!this.todoOpen) {
        if (this.$root.$children[0].activeIndex > -1) {
          const app = this.$root.$children[0].$children
          for (const el of app[app.length - 1].$children) {
            el.visible = true
          }
          app[app.length - 1].$children[this.$root.$children[0].activeIndex].todoOpen = true
          app[app.length - 1].$children[this.$root.$children[0].activeIndex].visible = false
          this.$root.$children[0].todoOpen = true
        }
      } else {
        const app = this.$root.$children[0].$children
        app[app.length - 1].$children[this.$root.$children[0].activeIndex].writeText = true
      }
    }
  }
}
</script>

<style lang="scss">

</style>
