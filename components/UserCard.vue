<template>
  <div class="author-card">
    <cs-profile
      avatar-position="left"
      :name="user.firstName"
      :detail="user.username"
      :style="{ '--cs-profile-background': '#F0F8FF' }"
    >
    </cs-profile>
    <cs-button class="remove-button" @click="onMakeAuthor"
      >Make Author</cs-button
    >
  </div>
</template>

<script>
export default {
  props: ["user"],
  methods: {
    async onMakeAuthor() {
      try {
        let data = {
          id: this.user._id,
          balance: 0,
          trust: 2.5,
        };
        let response = await this.$axios.$post(
          "http://localhost:3000/api/authors",
          data
        );

        if (response.success) {
          this.$emit("addAuthor", this.user);
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
