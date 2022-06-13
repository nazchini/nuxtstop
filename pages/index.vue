// latest articles about Nuxt will be listed here
<template>
  <div class="page-wrapper">
    <div class="article-cards-wrapper">
      <article-card-block
        v-for="(article, i) in articles"
        :key="article.id"
        :article="article"
        class="article-card-block"
      />
    </div>
  </div>
</template>

<script>
import ArticleCardBlock from "@/components/blocks/ArticleCardBlock";

export default {
  components: {
    ArticleCardBlock,
  },
  data() {
    return {
      currentPage: 1,
      articles: [],
    };
  },
  async fetch() {
    const articles = await fetch(
      `https://dev.to/api/articles?tag=nuxt&state=rising&page=${this.currentPage}`
    ).then((res) => res.json());

    this.articles = this.articles.concat(articles);
  },
};
</script>

<style lang="scss" scoped>
.page-wrapper {
  max-width: $screen-xl;
  margin: auto;
  padding: 1rem;
  min-height: 100vh;
}

.article-cards-wrapper {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
  .article-card-block {
    width: calc(100% - 2 * 1rem);
    margin: 1rem;
    margin-bottom: 1.5rem;
    margin-top: 0.5rem;
    @media (min-width: $screen-sm) {
      width: calc(50% - 2 * 1rem);
    }
    @media (min-width: $screen-lg) {
      width: calc(33.33333% - 2 * 1rem);
    }
  }
}
</style>
