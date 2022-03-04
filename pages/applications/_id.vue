<template>
  <div>
    <!-- {{ application }} -->
    <p>{{ application.userID._id }}</p>
    <p>{{ application.userID.firstName }} {{ application.userID.lastName }}</p>
    <p>{{ application.userID.username }}</p>
    <p>{{ application.description }}</p>
    <p>{{ application.status }}</p>
    <p>{{ application.title }}</p>
    <img :src="application.photo" alt="" class="img" />
    <div v-html="application.content"></div>
    <client-only>
      <cs-file-preview
        v-if="application.cv"
        :src="application.cv"
        file-type="application/pdf"
        :title="fileName"
      >
      </cs-file-preview>
      <cs-button @click="onAccept"> Accept </cs-button>
      <cs-button variant="danger" @click="onReject"> Reject </cs-button>
    </client-only>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    try {
      let response = await $axios.$get(
        `http://localhost:3000/api/applications/${params.id}`
      );
      return {
        application: response.application,
      };
    } catch (err) {
      console.log(err);
    }
  },
  computed: {
    fileName() {
      var n = this.application.cv.lastIndexOf("amazonaws.com/") + 13;
      var result = this.application.cv.substring(n + 1);
      return result;
    },
  },
  methods: {
    async onAccept() {
      try {
        let data = {
          id: this.application.userID._id,
          balance: 0,
          trust: 2.5,
        };
        let response = await this.$axios.$post(
          "http://localhost:3000/api/authors",
          data
        );

        if (response.success) {
          console.log("Author added");
          let response2 = await this.$axios.$delete(
            `http://localhost:3000/api/applications/${this.$route.params.id}`
          );
          if (response2.success) {
            this.$router.push("/cvs");
          }
        }
      } catch (err) {
        console.log(err);
      }
    },
    async onReject() {
      try {
        let response = await this.$axios.$delete(
          `http://localhost:3000/api/applications/${this.$route.params.id}`
        );
        if (response.success) {
          this.$router.push("/cvs");
        }
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style scoped>
.img {
  width: 300px;
  height: 300px;
}
</style>
