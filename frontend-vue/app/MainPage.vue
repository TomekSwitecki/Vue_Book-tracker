<script setup lang="ts">
import {ref,computed,onMounted} from "vue";
import type {Book} from "~/types/book";
import {AddBookForm} from "#components";
import {BookList} from "#components";

const books = ref<Book[]>([])
const search = ref('')

async function handleAddBook(book: Omit<Book, 'id'>) {
  const response = await fetch(
      'https://vuebook-tracker-production.up.railway.app/books',
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(book)
      }
  )

  const responseData = await response.json()

  books.value.push({
    id: responseData.id,
    ...book
  })

  search.value = ''
}

async function handleBookDelete(id: number) {
  try {
    await fetch(
        `https://vuebook-tracker-production.up.railway.app/books/${id}`,
        {
          method: 'DELETE'
        }
    )

    books.value = books.value.filter(
        book => book.id !== id
    )
  } catch (error) {
    console.error(error)
  }
}

const filteredBooks = computed(() => {
  return books.value.filter(book =>
      book.title.toLowerCase().includes(search.value.toLowerCase()) ||
      book.author.toLowerCase().includes(search.value.toLowerCase())
  )
})

//wykonaj ten kod, gdy komponent zostanie zamontowany w DOM.
onMounted(async () => {
  const response = await fetch(
      'https://vuebook-tracker-production.up.railway.app/books'
  )

  books.value = await response.json()
})




</script>

<template>
  <AddBookForm @add-book="handleAddBook"/>
  <div class="section-card">
    <div class="section-header">
      <h2>Search</h2>
    </div>

    <input
        v-model="search"
        type="text"
        placeholder="Search books..."
    >
  </div>
  <BookList :books="filteredBooks"
  @delete-book="handleBookDelete"/>
</template>


<style scoped>

</style>