<template>
  <div class="author-card">
    <cs-profile
      avatar-position="left"
      :name="author.userID.firstName"
      :detail="author.userID.username"
      :style="{ '--cs-profile-background': '#F0F8FF' }"
    >
    </cs-profile>
    <cs-button variant="danger" class="remove-button" @click="onRemoveAuthor"
      >Remove</cs-button
    >
  </div>
</template>

<script>
export default {
  props: ["author"],
  methods: {
    async onRemoveAuthor() {
      try {
        let response = await this.$axios.$delete(
          "http://localhost:3000/api/authors",
          { data: { id: this.author._id } }
        );
        if (response.success) {
          this.$emit("removeAuthor", this.author);
        }
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style scoped>
.author-card {
  position: relative;
}
.remove-button {
  position: absolute;
  top: 30%;
  bottom: 30%;
  right: 20px;
}
</style>
