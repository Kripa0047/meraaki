<template>
  <div class="new_post_container shadow">
    <Popup v-if="popup" v-bind:onClose="onClose" v-bind:text="popText" />
    <FullLoader v-if="loader" />

    <div class="new_post_header">Create new Post</div>
    <input
      class="input"
      @input="($event) => title = $event.target.value"
      type="text"
      placeholder="Title..."
      v-model="title"
    />
    <textarea
      class="input new_post_body"
      @input="($event) => message = $event.target.value"
      placeholder="What's on your mind..."
      v-model="message"
    />
    <div class="create_button">
      <div class="shadow" v-on:click="onCreateHandler">Create</div>
    </div>
  </div>
</template>

<script>
import FullLoader from "../Loaders/FullLoader";
import Popup from "../Popups/Popup";

export default {
  name: "NewPost",
  props: ["newPost"],
  components: {
    FullLoader,
    Popup,
  },
  data() {
    return {
      title: "",
      message: "",
      loader: false,
      popup: false,
      popText: "",
    };
  },
  methods: {
    onCreateHandler() {
      //   console.log(this.title, this.message);
      let title = this.title;
      let message = this.message;
      let isVerified = true;

      if (title.length === 0) {
        isVerified = false;
        this.popText = "Please enter the title!!!";
      }

      if (message.length === 0) {
        isVerified = false;
        this.popText = "Please write someting on the post!!!";
      }

      if (isVerified) {
        this.loader = true;
        fetch("https://jsonplaceholder.typicode.com/posts", {
          method: "POST",
          body: JSON.stringify({
            title: this.title,
            body: this.message,
            userId: 1,
          }),
          headers: {
            "Content-type": "application/json; charset=UTF-8",
          },
        })
          .then((response) => response.json())
          .then((json) => {
            this.loader = false;
            this.newPost(json);
            this.title = "";
            this.message = "";
            this.popText = "Post created successfully";
          })
          .catch(() => {
            this.loader = false;
            this.popText = "Something went wrong!!!";
          })
          .then(() => {
            this.popup = true;
          });
      } else {
        this.popup = true;
      }
    },
    onClose() {
      this.popup = false;
      this.popText = "";
    },
  },
};
</script>

<style scoped>
.new_post_container {
  padding: 20px;
  margin-bottom: 20px;
}

.new_post_header {
  text-align: center;
  padding: 10px;
  background-color: #383838;
  margin-bottom: 10px;
  border-radius: 5px;
  color: #636363;
  font-family: "GothicA1-Bold";
}

.input {
  width: 100%;
  padding: 10px;
  outline: none;
  border: 1px solid transparent;
  border-radius: 5px;
  background-color: #4b4b4b;
  color: #8f8f8f;
  margin-bottom: 10px;
  transition: 0.3s;
}

.input:focus {
  border-bottom-color: #bbbbbb;
}

.new_post_body {
  height: 150px;
}

.shadow {
  box-shadow: -3px -6px 10px 2px #383838, 3px 6px 10px 2px #222222;
}

.create_button {
  display: flex;
}

.create_button > div {
  padding: 7px 30px;
  background-color: #313131;
  border-radius: 5px;
  cursor: pointer;
  font-family: "GothicA1-Bold";
  color: #7c7c7c;
}

@font-face {
  font-family: "GothicA1-Bold";
  src: url("../../assets/fonts/GothicA1-Bold.ttf");
}
</style>
