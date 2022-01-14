<template>
  <div>
    <client-only>
      <Navbar
        class="navbar"
        :logo="logo"
        :links="links"
        :darkBackground="false"
        onHover="slide"
        logoTextClass="logo-text"
      />
    </client-only>
    <nuxt />
  </div>
</template>

<script>
import Navbar from "vue-navbar-component";
export default {
  components: {
    Navbar,
  },
  data() {
    return {
      logo: {
        img: "https://picsum.photos/203",
        text: "TRUSTER",
      },
      links: [
        {
          name: "Articles",
          click: () => this.$router.push("/"),
        },
        {
          name: "Authors",
          click: () => this.$router.push("/authors"),
        },
        {
          name: "Applications",
          click: () => this.$router.push("/cvs"),
        },
        {
          name: "Categories",
          click: () => this.$router.push("/categories"),
        },
      ],
    };
  },
};
</script>
<style></style>
