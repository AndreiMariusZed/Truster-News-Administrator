<template>
  <div>
    <client-only>
      <div class="add-category">
        <cs-input v-model="type"></cs-input>
        <cs-button class="add-category__button" @click="onAddCategory"
          >Add a new category</cs-button
        >
      </div>
      <categories-list :categories="categories" />
    </client-only>
  </div>
</template>

<script>
import CategoriesList from "../components/CategoriesList.vue";
export default {
  components: { CategoriesList },
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get("http://localhost:3000/api/categories");
      return {
        categories: response.categories,
      };
    } catch (err) {
      console.log(err);
    }
  },
  data() {
    return {
      type: "",
    };
  },
  methods: {
    async onAddCategory() {
      try {
        let data = { type: this.type };
        let response = await this.$axios.$post(
          "http://localhost:3000/api/categories",
          data
        );
        if (response.success) {
          this.categories.push(data);
        }
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style scoped>
.add-category {
  margin: 10px;
  display: flex;
}
</style>
