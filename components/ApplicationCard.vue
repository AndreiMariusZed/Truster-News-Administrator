<template>
  <div class="application-card" @click="goToApplicationDetail">
    <!-- {{ application }} -->
    <p>{{ application.userID.firstName }} {{ application.userID.lastName }}</p>
    <p>{{ application.userID.username }}</p>
    <p>{{ application.description }}</p>
    <p>{{ application.status }}</p>
    <p>{{ application.cv }}</p>
  </div>
</template>

<script>
export default {
  props: ["application"],
  methods: {
    goToApplicationDetail() {
      this.$router.push(`/applications/${this.application._id}`);
    },
  },
};
</script>

<style scoped>
.application-card {
  background: aquamarine;
  padding: 10px;
  margin: 10px;
}
</style>
