<template>
  <div>
    <cs-article-card
      picture-position="top"
      :picture="article.photo"
      :title="article.title"
      :summary="article.content"
      author="Monica Geller"
      duration="3 min"
    >
      <i class="cs-icons-delete" slot="options"></i>
      <i class="cs-icons-edit" slot="options"></i>
      <i class="cs-icons-share" slot="options"></i>
    </cs-article-card>
  </div>
</template>

<script>
export default {
  props: ["article"],
};
</script>

<style scoped>
i {
  cursor: pointer;
}
</style>
