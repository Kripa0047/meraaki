<template>
  <div class="full_loader_container">
    <Loader class="loader" />
  </div>
</template>

<script>
import Loader from "./Loader";

export default {
  name: "FullLoader",
  components: {
    Loader,
  },
};
</script>

<style scoped>
.full_loader_container {
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  background-color: #5e5e5e5d;
}

.loader {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
