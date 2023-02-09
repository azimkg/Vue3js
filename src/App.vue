<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <my-button @click="showDialog">Создать пост </my-button>
    <my-dialog v-model:show="dialogVis">
      <post-form @create="createPost" />
    </my-dialog>

    <post-list :posts="posts" @remove="removePost" />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";

export default {
  components: {
    PostList,
    PostForm,
  },
  data() {
    return {
      posts: [
        { id: 1, title: "JavaScript", body: "Описание поста 1" },
        { id: 2, title: "Python", body: "Описание поста 2" },
        { id: 3, title: "Ruby", body: "Описание поста 3" },
      ],
      dialogVis: false,
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVis = false;
    },
    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showDialog() {
      this.dialogVis = true;
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
</style>
