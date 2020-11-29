<template lang='pug'>
div
| Username: {{user.username}}
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'YuriiTrofimenko',
        firstName: 'Yurii',
        lastName: 'Trofimenko',
        email: 'tyaa@ukr.net',
        isAdmin: true
      }
    }
  }
}
</script>

<style lang='stylus'>
#app 
	font-family Avenir, Helvetica, Arial, sans-serif
	-webkit-font-smoothing antialiased
	-moz-osx-font-smoothing grayscale
	text-align center
	color #2c3e50
	margin-top 60px
</style>
