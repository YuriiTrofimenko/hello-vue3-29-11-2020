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
    form.create-article-panel(@submit.prevent="createNewArticle")
      label(for="newArticle")
        strong New Article
      textarea#newArticle(rows="4" v-model="newArticleContent")
      .create-article-type
        label(for="newArticleType")
          strong Type: 
        select#newArticleType(v-model="selectedArticleType")
          option(:value="option.value" v-for="(option, index) in articleTypes" :key="index")
            | {{ option.name }}
      .create-article-panel__submit
        button
          | Add
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
      favouriteArticleId: null,
      articleTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Article'}
      ],
      newArticleContent: '',
      selectedArticleType: 'instant',
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
    },
    createNewArticle () {
      if (this.newArticleContent && this.selectedArticleType !== 'draft') {
        this.user.articles.unshift(
          {
            id: this.user.articles.length + 1,
            title: 'Title stub',
            content: this.newArticleContent
          }
        )
      }
      this.newArticleContent = ''
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

.create-article-panel
  margin-top 20px
  padding 20px 0
  display flex
  flex-direction column
  textarea
    border 1px solid #dfe3e8
    border-radius 5px
  .create-article-panel__submit
    display flex
    justify-content space-between
    .create-article-type
      padding 10px 0
    button
      padding 5px 20px
      margin auto 0
      border-radius 5px
      border none
      background-color #6c9
      color white
      font-weight bold
</style>
