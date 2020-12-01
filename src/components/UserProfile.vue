<template lang='pug'>
.user-profile
  .user-profile__user-panel
    h1.user-profile__username @{{ user.username }}
    .user-profile__follower-count
      strong Followers: {{followers}}
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
.user-profile
  display grid
  grid-template-columns 1fr 3fr
  grid-gap 50px
  padding 50px 5%

  .user-profile__user-panel
    display flex
    flex-direction column
    padding 20px
    background-color white
    border-radius 5px
    border 1px solid #DFE3E8
    margin-bottom auto

    h1
      margin 0
</style>
