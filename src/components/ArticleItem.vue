<template lang="pug">
.article-item
  .user-profile__article
    .article-item__title
    |{{ article.title }}
    .article-item__content
    |{{ article.content }}
</template>

<script>
export default {
  name: "ArticleItem",
  props: {
    article: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="stylus" scoped>
.article-item
  padding 20px
  background-color white
  border-radius 5px
  border 1px solid #dfe3f8
  box-sizing border-box
  cursor pointer
  transition all 0.25s ease

  &:hover
    transform scale(1.1, 1.1)

  .article-item__title
    font-weight bold
</style>