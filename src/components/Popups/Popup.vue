<template>
  <div class="popup_container">
    <div class="close_pop" v-on:click="onClose"></div>
    <div class="pop_content">{{text}}</div>
  </div>
</template>

<script>
export default {
  name: "Popup",
  props: ["onClose", "text"],
};
</script>

<style scoped>
.popup_container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: #3b3b3b57;
}

.close_pop {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100vw;
  height: 100vh;
  cursor: pointer;
}

.pop_content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 10px;
  width: 250px;
  text-align: center;
  background-color: #292929;
  border-radius: 5px;
  color: #7e7e7e;
}

@font-face {
  font-family: "GothicA1-Regular";
  src: url("../../assets/fonts/GothicA1-Regular.ttf");
}
</style>
