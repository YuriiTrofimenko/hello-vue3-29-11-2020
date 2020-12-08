<template lang='pug'>
.user-profile
  .user-profile__user-panel
    h1.user-profile__username @{{ state.user.username }}
    .user-profile__admin-badge(v-if="state.user.isAdmin")
      |Admin
    .user-profile__admin-badge(v-else)
      |User
    .user-profile__follower-count
      strong Followers: {{state.followers}}
    ArticleForm(@add-article="addArticle")
  .user-profile__articles-wrapper
    ArticleItem(v-for="article in state.user.articles" :key="article.id" :article="article")
</template>

<script>
import { reactive, computed } from 'vue'
import { useRoute } from 'vue-router'
import ArticleForm from '../components/ArticleForm'
import ArticleItem from '../components/ArticleItem'
import { users } from '../assets/users'
export default {
  name: 'UserProfile',
  components: { ArticleItem, ArticleForm },
  setup () {
    const route = useRoute()
    const userId = computed(() => route.params.userId)
    const state = reactive({
      followers: 0,
      user: users.find(u => u.id.toString() === userId.value) || users[0],
      favouriteArticleId: null,
    })
    function addArticle(newArticleContent) {
      state.user.articles.unshift({
        id: state.user.articles.length + 1,
        title: 'Title stub',
        content: newArticleContent
      })
    }
    return {
      state,
      addArticle
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
