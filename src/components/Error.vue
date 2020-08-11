<template>
  <div class="error_conatiner">
    <div class="error shadow">Something went wrong!!!</div>
  </div>
</template>

<script>
export default {
  name: "Error",
};
</script>

<style scoped>
.error_conatiner {
  display: flex;
  justify-content: center;
}

.error {
  font-size: 130%;
  padding: 10px 20px;
  color: #888888;
}

.shadow {
  box-shadow: -3px -6px 10px 2px #383838, 3px 6px 10px 2px #222222;
}
</style>
