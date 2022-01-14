<template>
  <div>
    <author-card
      v-for="author in authors"
      :key="author._id"
      :author="author"
      @removeAuthor="removeAuthor"
    />
  </div>
</template>

<script>
import AuthorCard from "./AuthorCard.vue";
export default {
  components: { AuthorCard },
  props: ["authors"],
  methods: {
    removeAuthor(author) {
      this.$emit("removeAuthor", author);
    },
  },
};
</script>

<style></style>
