<template lang='pug'>
.app
  UserProfile
</template>

<script>
import UserProfile from './components/UserProfile'
export default {
  name: 'App',
  components: { UserProfile },
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
  mounted () {
    this.followUser()
  },
  computed: {
    fullName () {
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  watch: {
    followers(newFollowersCount, oldFollowersCount) {
      if(newFollowersCount < oldFollowersCount) {
        alert(`User ${this.user.username} has gained a follower`)
      }
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
	color #2c3e50
	min-height 100vh
	background-color #f3f5fa
</style>
