<template>
  <div>
    <client-only v-if="articles">
      <articles-list :articles="articles" />
    </client-only>
  </div>
</template>

<script>
import ArticlesList from "../components/ArticlesList.vue";
export default {
  layout: "default",
  components: { ArticlesList },
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get("http://localhost:3000/api/articles");
      return {
        articles: response.articles,
      };
    } catch (err) {
      console.log(err);
    }
  },
};
</script>
