<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="app__btns">
      <my-button @click="showDialog">Создать пост </my-button>
      <my-select :model-value="selectedSort" :options="sortOptions" />
    </div>
    <my-dialog v-model:show="dialogVis">
      <post-form @create="createPost" />
    </my-dialog>
    <post-list :posts="posts" @remove="removePost" v-if="!isPostLoading" />
    <div v-else>Идет загрузка...</div>
    <div class="page__wrapper">
      <div
        class="page"
        :class="{
          current__page: page === pageNum,
        }"
        v-for="pageNum in totalPage"
        @click="changePage(pageNum)"
      >
        {{ pageNum }}
      </div>
    </div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from "axios";

export default {
  components: {
    PostList,
    PostForm,
  },
  data() {
    return {
      posts: [],
      dialogVis: false,
      isPostLoading: false,
      selectedSort: "",
      page: 1,
      limit: 10,
      totalPage: 0,
      sortOptions: [
        {
          value: "title",
          name: "По названию",
        },
        {
          value: "body",
          name: "По описанию",
        },
      ],
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
    changePage(pageNum) {
      this.page = pageNum;
      this.fetchPost();
    },
    async fetchPost() {
      try {
        this.isPostLoading = true;

        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _page: this.page,
              _limit: this.limit,
            },
          }
        );
        this.totalPage = Math.ceil(res.headers["x-total-count"] / this.limit);
        this.posts = res.data;
      } catch (e) {
        alert(e);
      } finally {
        this.isPostLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPost();
  },
  computed: {
    sortPosts() {
      [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(
          post2[this.selectedSort]
        );
      });
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
.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
.page__wrapper {
  display: flex;
  margin-top: 15px;
}
.page {
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
}
.current__page {
  background: teal;
  color: white;
}
</style>
