<template>
  <div class="loader_container">
      <div class="bar one"></div>
      <div class="bar two"></div>
      <div class="bar three"></div>
  </div>
</template>

<script>
export default {
  name: "Loader",
};
</script>

<style scoped>
    .loader_container  {
        padding: 20px 0;
        display: flex;
        align-items: center;
        justify-content: center;
        height: 25px;
    }

    .bar    {
        height: 25px;
        width: 3px;
        background-color: #ffffff;
        margin: 0 2px;
        border-radius: 3px;
    }

    .one    {
        animation: bar 1.5s infinite;
    }

    .two    {
        animation: bar 1.5s infinite .3s;
    }

    .three    {
        animation: bar 1.5s infinite .6s;
    }

    @keyframes bar {
        0%  {
            height: 25px;
        }

        50% {
            height: 5px;
        }

        100%    {
            height: 25px;
        }
    }
</style>
