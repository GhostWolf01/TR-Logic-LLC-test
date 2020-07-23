<template>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 32 32" width="32" height="32"><title>{{title}}</title><g stroke-linecap="square" stroke-linejoin="miter" stroke-width="2" fill="#111111" stroke="#111111"><line x1="20" y1="5" x2="27" y2="12" fill="none" stroke-miterlimit="10" stroke-linecap="butt"/>
    <line x1="3" y1="22" x2="10" y2="29" fill="none" stroke-miterlimit="10" stroke-linecap="butt"/>
    <line x1="6.5" y1="25.5" x2="23.5" y2="8.5" fill="none" stroke-miterlimit="10" stroke-linecap="butt"/>
    <path d="M10,29,2,30l1-8L22.586,2.414a2,2,0,0,1,2.828,0l4.172,4.172a2,2,0,0,1,0,2.828Z" fill="none" stroke="#111111" stroke-miterlimit="10"/></g>
  </svg>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'pencil'
    }
  }
}
</script>

<style lang="scss">
  svg{
    margin-right: 10px;
    cursor: pointer;
  }
</style>
