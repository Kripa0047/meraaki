<template>
  <div id="app">
    <MainPage />
  </div>
</template>

<script>
import MainPage from "./components/MainPage";

export default {
  name: "App",
  components: {
    MainPage,
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "GothicA1-Regular";
}

#app {
  background-color: #313131;
  min-height: 100vh;
}

*::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  border-radius: 10px;
  background-color: #686868;
}

*::-webkit-scrollbar {
  width: 8px;
  background-color: #686868;
}

*::-webkit-scrollbar-thumb {
  border-radius: 10px;
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  background-color: #535353;
}

@font-face {
  font-family: "GothicA1-Regular";
  src: url("./assets/fonts/GothicA1-Regular.ttf");
}
</style>
