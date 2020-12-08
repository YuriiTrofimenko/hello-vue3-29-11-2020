<template lang="pug">
.app
  nav
    router-link(to="/") Home
    router-link(to="/user/1") User
  <router-view/>
</template>

<style lang="stylus">
.app 
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  color #2c3e50
  min-height 100vh
  background-color #f3f5fa

  nav
    display flex
    align-items center
    padding 10px 5%
    background-color #333
    color white

    a
      margin-right 10px
</style>
