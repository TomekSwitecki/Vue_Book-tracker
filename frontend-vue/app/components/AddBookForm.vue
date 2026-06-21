<script setup lang="ts">
import {ref} from "vue";
import type {Book} from "~/types/book";

const emit = defineEmits<{
  //addBook: [book: NewBook]
  addBook: [book:Omit<Book,"id">]
}>()

const title = ref('')
const author = ref('')
const isbn = ref('')
const pages = ref('')
const rating = ref('')


function handleSubmit(){
  if (!title.value.trim()) {
    alert('Title is required')
    return
  }

  if (!author.value.trim()) {
    alert('Author is required')
    return
  }

  if (!isbn.value.trim()) {
    alert('ISBN is required')
    return
  }

  if (Number(pages.value) < 1) {
    alert('Pages must be greater than 0')
    return
  }

  if (Number(rating.value) < 1) {
    alert('Rating must be greater than 0')
    return
  }


  emit('addBook',{
    title: title.value,
    author: author.value,
    isbn: isbn.value,
    pages: Number(pages.value),
    rating: Number(rating.value)
  })



  title.value = ''
  author.value = ''
  isbn.value = ''
  pages.value = ''
  rating.value = ''
}


</script>

<template>
  <div class="section-card">
    <div class="section-header">
      <div class="section-header__icon">
        <svg
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="none"
        >
          <circle
              cx="12"
              cy="12"
              r="10"
              stroke="#3B6FE0"
              stroke-width="2"
          />
          <line
              x1="12"
              y1="8"
              x2="12"
              y2="16"
              stroke="#3B6FE0"
              stroke-width="2"
              stroke-linecap="round"
          />
          <line
              x1="8"
              y1="12"
              x2="16"
              y2="12"
              stroke="#3B6FE0"
              stroke-width="2"
              stroke-linecap="round"
          />
        </svg>
      </div>

      <h2>Add Book</h2>
    </div>
    <form
        class="input-form"
        @submit.prevent="handleSubmit"
    >
      <input
          v-model="title"
          placeholder="Title"
      >

      <input
          v-model="author"
          placeholder="Author"
      >

      <input
          v-model="isbn"
          placeholder="ISBN"
      >

      <input
          v-model="pages"
          type="number"
          placeholder="Pages"
      >

      <input
          v-model="rating"
          type="number"
          min="1"
          max="5"
          placeholder="Rating (1–5)"
      >

      <button
          class="button"
          type="submit"
      >
        Add Book
      </button>
    </form>
  </div>
</template>

<style lang="scss">
.input-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}


</style>