<template>
  <div class="post_card shadow" v-on:click="commentsHandler(post.id)">
    <h2 class="title">{{post.title}}</h2>
    <p class="body">{{post.body}}</p>

    <div v-if="showComments" class="comments_container shadow">
      <div class="comment_header">Comments</div>
      <div class="comments">
        <div class="comment" v-for="comment in comments" v-bind:key="comment.id">
          <div class="details">
            <div class="name">{{comment.name}}</div>
            <div class="email">{{comment.email}}</div>
          </div>
          <div class="comment_body body">{{comment.body}}</div>
        </div>
      </div>

      <Loader v-if="loading" />

      <Error v-if="error" />
    </div>
  </div>
</template>

<script>
import Loader from "../Loaders/Loader";
import Error from "../Error";

export default {
  name: "PostCard",
  props: ["post"],
  components: {
    Loader,
    Error,
  },
  data() {
    return {
      showComments: false,
      comments: [],
      loading: false,
      error: false,
    };
  },
  methods: {
    commentsHandler(id) {
      this.showComments = !this.showComments;

      if (this.showComments) {
        // console.log("showing..");
        this.loading = true;
        this.error = false;
        fetch(`https://jsonplaceholder.typicode.com/posts/${id}/comments`)
          .then((response) => response.json())
          .then((json) => {
            this.loading = false;
            this.comments = json;
            // console.log(json);
          })
          .catch(() => {
            this.loading = false;
            this.error = true;
            // console.log(error);
          });
      }
    },
  },
};
</script>

<style scoped>
.post_card {
  margin: 30px 0;
  padding: 10px 20px;
  background-color: #313131;
  border-radius: 10px;
  cursor: pointer;
}

.title {
  margin: 10px 0;
  text-transform: uppercase;
  color: #dadada;
  font-size: 120%;
}

.body {
  font-size: 90%;
  color: #b4b4b4;
  font-family: "GothicA1-Light";
}

.shadow {
  box-shadow: -3px -6px 10px 2px #383838, 3px 6px 10px 2px #222222;
}

.comments_container {
  padding: 10px 20px;
  margin-top: 20px;
  border-radius: 10px;
}

.comment_header {
  font-family: "GothicA1-Bold";
  color: #868686;
}

.comment {
  margin: 10px 20px;
  padding-bottom: 10px;
  border-bottom: 1px solid #464646;
}

.details {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
}

.name,
.email {
  font-size: 80%;
}

.name {
  color: #9e9e9e;
  font-family: "GothicA1-SemiBold";
}

.email {
  color: #868686;
}

.comment_body {
  color: #c7c7c7;
}

@media only screen and (max-width: 760px) {
  .comment {
    margin: 10px;
  }

  .details {
    flex-direction: column;
    align-items: flex-start;
  }
}

@font-face {
  font-family: "GothicA1-Light";
  src: url("../../assets/fonts/GothicA1-Light.ttf");
}

@font-face {
  font-family: "GothicA1-Bold";
  src: url("../../assets/fonts/GothicA1-Bold.ttf");
}

@font-face {
  font-family: "GothicA1-SemiBold";
  src: url("../../assets/fonts/GothicA1-SemiBold.ttf");
}
</style>
