<template>
  <div>
    <category-card
      v-for="category in categories"
      :key="category._id"
      :category="category"
    />
  </div>
</template>

<script>
import CategoryCard from "./CategoryCard.vue";
export default {
  components: { CategoryCard },
  props: ["categories"],
};
</script>

<style scoped></style>
