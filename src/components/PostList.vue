<template>
  <div v-if="posts.length > 0">
    <h3>Список ползователей</h3>
    <post-item
      :key="post.id"
      :post="post"
      @remove="$emit('remove', post)"
      v-for="post in posts"
    />
  </div>
  <h3 v-else class="title">Список пользователей пуст</h3>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoaped>
.title {
  color: red;
}
</style>
