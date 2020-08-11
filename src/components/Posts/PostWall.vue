<template>
  <div>
    <Loader v-if="loading" />

    <Error v-if="error" />

    <div v-if="posts">
      <PostCard v-for="(post, index) in posts" v-bind:key="index" v-bind:post="post"></PostCard>
    </div>
  </div>
</template>

<script>
import Loader from "../Loaders/Loader";
import PostCard from "./PostCard";
import Error from "../Error";

export default {
  name: "PostWall",
  props: ["props_posts", "getPosts"],
  components: {
    Loader,
    PostCard,
    Error,
  },
  data() {
    return {
      loading: false,
      posts: this.props_posts,
      error: false,
    };
  },
  created() {
    this.fetchData();
  },
  watch: {
    props_posts: function (newVal) {
      this.posts = newVal;
    },
  },
  methods: {
    fetchData() {
      this.error = this.post = null;
      this.loading = true;
      this.error = false;
      fetch("https://jsonplaceholder.typicode.com/posts")
        .then((response) => response.json())
        .then((json) => {
          this.loading = false;
          // this.posts = json;
          this.getPosts(json);
          // console.log(json);
        })
        .catch(() => {
          this.loading = false;
          this.error = true;
          this.posts = JSON.parse(localStorage.getItem('storedPosts'));
          // console.log(error);
        });
    },
  },
};
</script>

<style scoped>
</style>
