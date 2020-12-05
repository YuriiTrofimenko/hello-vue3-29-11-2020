<template lang='pug'>
form.create-article-panel(@submit.prevent="createNewArticle" :class="{ '--exceeded': newArticleCharacterCount > 180 }")
  label(for="newArticle")
    strong New Article
    |  ({{ newArticleCharacterCount }}/180)
  textarea#newArticle(rows="4" v-model="state.newArticleContent")
  .create-article-type
    label(for="newArticleType")
      strong Type: 
    select#newArticleType(v-model="state.selectedArticleType")
      option(:value="option.value" v-for="(option, index) in state.articleTypes" :key="index")
        | {{ option.name }}
  .create-article-panel__submit
    button
      | Add
</template>

<script>
import { reactive, computed } from 'vue'
export default {
  name: "ArticleForm",
  setup (props, ctx) {
    const state = reactive({
      articleTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Article'}
      ],
      newArticleContent: '',
      selectedArticleType: 'instant',
    })
    const newArticleCharacterCount = computed(() => state.newArticleContent.length)
    function createNewArticle () {
      if (state.newArticleContent && state.selectedArticleType !== 'draft') {
        ctx.emit('add-article', state.newArticleContent)
        state.newArticleContent = ''
      }
    }
    return {
      state,
      newArticleCharacterCount,
      createNewArticle
    }
  }
}
</script>

<style lang='stylus'>
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
  &.--exceeded
    color red
    border-color red
    .create-article-panel__submit
      button
        background-color red
        color white
</style>