<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <my-input v-model:value="post.title" type="text" placeholder="Title" />
    <my-input v-model:value="post.body" type="text" placeholder="Description" />
    <my-button @click="createPost">Добавить</my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        title: "",
        body: "",
      };
    },
  },
};
</script>

<style>
form {
  display: flex;
  flex-direction: column;
}
</style>
