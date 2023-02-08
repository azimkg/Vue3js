<template>
  <div class="post" v-for="post in posts">
    <div><strong>Title:</strong>{{ post.title }}</div>
    <div><strong>Description:</strong>{{ post.body }}</div>
  </div>
</template>

<script></script>

<style scoaped>
.post {
  margin: 15px;
  padding: 15px;
  border: 2px solid teal;
}
</style>
