<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <input
      v-bind:value="title"
      @input="title = $event.target.value"
      class="input"
      type="text"
      placeholder="Title"
    />
    <input
      v-bind:value="body"
      @input="body = $event.target.value"
      class="input"
      type="text"
      placeholder="Description"
    />
    <button @click="addPost" class="btn">Добавить</button>
  </form>
</template>

<script></script>

<style></style>
