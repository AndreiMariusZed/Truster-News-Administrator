<template>
  <div class="category-card">
    <cs-profile
      avatar-position="left"
      :name="category.type"
      :style="{ '--cs-profile-background': '#F0F8FF' }"
    >
    </cs-profile>
    <cs-button variant="danger" class="remove-button">Remove</cs-button>
  </div>
</template>

<script>
export default {
  props: ["category"],
};
</script>

<style scoped>
.category-card {
  position: relative;
  margin-bottom: 10px;
}
.remove-button {
  position: absolute;
  top: 30%;
  bottom: 30%;
  right: 20px;
}
</style>
