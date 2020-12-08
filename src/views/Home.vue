<template lang='pug'>
.home
  h1 Home
  .users-list
    router-link(v-for="user in users" :to="{ name: 'UserProfile', params: { userId: user.id } }" :key="user.id")
      |{{ user.username }}
</template>

<script>
import {users} from "../assets/users"
export default {
  name: 'Home',
  setup() {
    return {
      users
    }
  }
}
</script>

<style lang="stylus" scoped>
.home
  padding 50px 5%
  .users-list
    display flex
    flex-direction column
</style>
