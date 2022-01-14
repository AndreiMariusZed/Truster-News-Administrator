<template>
  <div>
    <user-card
      v-for="user in users"
      :key="user._id"
      :user="user"
      @addAuthor="addAuthor"
    />
  </div>
</template>

<script>
import UserCard from "./UserCard.vue";
export default {
  components: { UserCard },
  props: ["users"],
  methods: {
    addAuthor(user) {
      this.$emit("addAuthor", user);
    },
  },
};
</script>

<style></style>
