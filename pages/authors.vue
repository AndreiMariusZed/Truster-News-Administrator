<template>
  <div>
    <client-only>
      <p>USERS</p>
      <users-list :users="users" @addAuthor="addAuthor" />
      <br />
      <p>AUTHORS</p>
      <authors-list :authors="authors" @removeAuthor="removeAuthor" />
    </client-only>
  </div>
</template>

<script>
import AuthorsList from "../components/AuthorsList.vue";
import UsersList from "../components/UsersList.vue";
export default {
  components: { AuthorsList, UsersList },
  async asyncData({ $axios }) {
    try {
      let users = $axios.$get("http://localhost:3000/api/users");
      let authors = $axios.$get("http://localhost:3000/api/authors");

      const [usersResponse, authorsResponse] = await Promise.all([
        users,
        authors,
      ]);

      return {
        users: usersResponse.users,
        authors: authorsResponse.authors,
      };
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async addAuthor(user) {
      let indexOfUser = this.users.indexOf(user);
      this.users.splice(indexOfUser, 1);
      let data = {
        id: user._id,
      };
      try {
        let response = await this.$axios.$get(
          `http://localhost:3000/api/authors/${user._id}`
        );
        this.authors.push(response.author);
      } catch (err) {
        console.log(err);
      }
    },
    async removeAuthor(author) {
      let indexOfAuthor = this.authors.indexOf(author);
      this.authors.splice(indexOfAuthor, 1);
      this.users.push(author.userID);
    },
  },
};
</script>

<style></style>
