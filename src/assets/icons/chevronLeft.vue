<template>
<svg @click="back()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48"><title>{{title}}</title>
    <g fill="#000000">
        <path d="M30.83 14.83L28 12 16 24l12 12 2.83-2.83L21.66 24z"/>
    </g>
</svg>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'chevron left'
    }
  },
  methods: {
    back () {
      const app = this.$root.$children[0].$children
      for (const el of app[app.length - 1].$children) {
        el.active = false
        el.visible = false
        el.todoOpen = false
      }
      this.$root.$children[0].activeIndex = -1
    }
  }
}
</script>

<style lang="scss" scoped>
svg{
  border: 2px solid rgba($color: #ffc107, $alpha: 0.6);
  border-radius: 50%;
  &:hover{
    background-color: rgba($color: #343a40, $alpha: 0.6);
  }
}
</style>
