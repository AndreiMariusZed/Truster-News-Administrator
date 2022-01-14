<template>
  <div>
    <application-card
      v-for="application in applications"
      :key="application._id"
      :application="application"
    />
  </div>
</template>

<script>
import ApplicationCard from "./ApplicationCard.vue";
export default {
  components: { ApplicationCard },
  props: ["applications"],
};
</script>

<style></style>
