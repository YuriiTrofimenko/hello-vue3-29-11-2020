<template lang='pug'>
.user-profile
  .user-profile__user-panel
    h1.user-profile__username @{{ user.username }}
    .user-profile__admin-badge(v-if="user.isAdmin")
      |Admin
    .user-profile__admin-badge(v-else)
      |User
    .user-profile__follower-count
      strong Followers: {{followers}}
    div(v-if="favouriteArticleId")
      |Favourite article is "{{user.articles.find(a => a.id === favouriteArticleId).title}}"
  .user-profile__articles-wrapper
    ArticleItem(v-for="article in user.articles" :key="article.id" :article="article" @favourite="toggleFavourite")
</template>

<script>
import ArticleItem from './ArticleItem'
export default {
  name: 'UserProfile',
  components: { ArticleItem },
  data () {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'YuriiTrofimenko',
        firstName: 'Yurii',
        lastName: 'Trofimenko',
        email: 'tyaa@ukr.net',
        isAdmin: false,
        articles: [
          { id: 1, title: 'Hello VUE 3!', content: '1 - lorem ipsum dolor sit amet' },
          { id: 2, title: 'Lorem ipsum dolor', content: '2 - lorem ipsum dolor sit amet'  },
          { id: 3, title: 'The third article', content: '3 - lorem ipsum dolor sit amet'  }
        ]
      },
      favouriteArticleId: null
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
    },
    toggleFavourite (id) {
      this.favouriteArticleId = id
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

    .user-profile__admin-badge
      background darkgreen
      color white
      border-radius 5px
      margin-right auto
      padding 0 10px
      font-weight bold

  .user-profile__articles-wrapper
    display grid
    grid-gap 10px
    margin-bottom auto
</style>
