<template>
  <div><applications-list :applications="applications" /></div>
</template>

<script>
import ApplicationsList from "../components/ApplicationsList.vue";
export default {
  components: { ApplicationsList },
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get(
        "http://localhost:3000/api/applications"
      );
      return {
        applications: response.applications,
      };
    } catch (err) {
      console.log(err);
    }
  },
};
</script>

<style></style>
