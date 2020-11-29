<template lang='pug'>
.app
  span Username {{user.username}} - {{fullName}}
  strong Followers: {{followers}}
  button(@click="followUser") follow
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
  },
  computed: {
    fullName () {
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods: {
    followUser () {
      this.followers++
    }
  }
}
</script>

<style lang='stylus'>
.app 
	font-family Avenir, Helvetica, Arial, sans-serif
	-webkit-font-smoothing antialiased
	-moz-osx-font-smoothing grayscale
	display flex
	flex-direction column
	text-align center
	color #2c3e50
</style>
