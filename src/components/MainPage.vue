<template>
  <div class="container">
    <div class="main_title">
      <div>MERAAKI</div>
      <div class="bar">
        <div class="sub_bar"></div>
      </div>
    </div>
    <NewPost v-bind:newPost="appendNewPost" />
    <PostWall v-bind:props_posts="posts" v-bind:getPosts="getPosts" />
  </div>
</template>

<script>
import PostWall from "./Posts/PostWall";
import NewPost from "./Posts/NewPost";

export default {
  name: "MainPage",
  data() {
    return {
      posts: [],
    };
  },
  components: {
    PostWall,
    NewPost,
  },
  methods: {
    appendNewPost(newPost) {
      // console.log(newPost);
      let oldPosts = [...this.posts];
      let newPosts = [newPost].concat(oldPosts);
      // let newPosts = oldPosts.push(newPost);
      // console.log(newPosts);
      this.posts = newPosts;
    },

    getPosts(posts) {
      let newPosts = [...posts];
      this.posts = newPosts;
      localStorage.setItem("storedPosts", JSON.stringify(posts));
      // console.log(sp);
    },
  },
};
</script>

<style scoped>
.container {
  padding: 20px 20%;
  color: #ffffff;
}

.main_title {
  padding: 20px;
  text-align: center;
  font-size: 150%;
  color: #8d8d8d;
  font-family: "GothicA1-Bold";
  display: flex;
  flex-direction: column;
  align-items: center;
}

.bar {
  width: 100px;
  height: 5px;
  background-color: #8d8d8d;
  position: relative;
  overflow: hidden;
  border-radius: 2px;
}

.sub_bar {
  width: 12px;
  height: 5px;
  position: absolute;
  background-color: inherit;
  border-left: 3px solid #2c2c2c;
  border-right: 3px solid #2c2c2c;
  left: -10px;
  animation: slide 3s infinite;
}

@media only screen and (max-width: 1200px) {
  .container {
    padding: 20px 15%;
  }
}

@media only screen and (max-width: 1000px) {
  .container {
    padding: 20px 10%;
  }
}

@media only screen and (max-width: 760px) {
  .container {
    padding: 20px;
  }
}

@font-face {
  font-family: "GothicA1-Bold";
  src: url("../assets/fonts/GothicA1-Bold.ttf");
}

@keyframes slide {
  0%  {
    left: -10px;
  }
  100%  {
    left: 110px;
  }
}
</style>
