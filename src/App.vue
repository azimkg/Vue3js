<template>
  <div class="app"></div>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        { id: 1, title: "JavaScript", body: "Описание поста 1" },
        { id: 2, title: "Python", body: "Описание поста 2" },
        { id: 3, title: "Ruby", body: "Описание поста 3" },
      ],
      title: "",
      body: "",
    };
  },
  methods: {
    addPost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body,
      };
      this.posts.push(newPost);
      this.title = "";
      this.body = "";
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.post {
  margin: 15px;
  padding: 15px;
  border: 2px solid teal;
}
.app {
  padding: 20px;
}
form {
  display: flex;
  flex-direction: column;
}
.btn {
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  margin-top: 15px;
  color: teal;
  border: 1px solid teal;
}
.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>
