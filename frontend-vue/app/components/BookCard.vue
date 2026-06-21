<script setup lang="ts">
import type {Book} from "~/types/book";
import {StarRating} from "#components";

const props = defineProps<{
  book:Book
}>()

const emit = defineEmits<{
  delete: [id: number]
}>()

function handleDelete(){
  emit("delete",props.book.id)
}

</script>

<template>
  <div class="book-item">
    <div class="book-item__thumbnail">
      <svg width="26" height="26" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20" stroke="#3B6FE0" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" />
        <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z" stroke="#3B6FE0" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" />
      </svg>
    </div>

    <div class="book-item__main">
      <h3>{{ book.title }}</h3>
      <p>{{ book.author }}</p>
      <p class="book-item__isbn">ISBN: {{ book.isbn }}</p>
    </div>

    <div class="book-item__details">
      <p class="book-item__pages"><span>Pages:</span> {{book.pages}}</p>
      <StarRating :rating="book.rating"/>
    </div>

    <button class="button button--remove" @click="handleDelete()" aria-label="Delete book">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <polyline points="3 6 5 6 21 6" stroke="#e05353" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" />
      <path d="M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6" stroke="#e05353" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" />
      <path d="M10 11v6M14 11v6" stroke="#e05353" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" />
      <path d="M9 6V4a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v2" stroke="#e05353" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" />
    </svg>
    </button>
  </div>
</template>

<style lang="scss">
.book-item__wrapper {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.book-item {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 14px 0;
  border-bottom: 1.5px solid #f0f2f7;

  &:last-child {
    border-bottom: none;
    padding-bottom: 0;
  }

  &:first-child {
    padding-top: 0;
  }
}

.book-item__thumbnail {
  width: 52px;
  height: 52px;
  background: #eef2fc;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.book-item__main {
  display: flex;
  flex-direction: column;
  gap: 3px;
  flex: 1;
  min-width: 0;

  h3 {
    font-size: 15px;
    font-weight: 700;
    color: #1a1a2e;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  p {
    font-size: 13px;
    color: #6b7280;
  }
}

.book-item__isbn {
  font-size: 12px !important;
  color: #b0b5c4 !important;
}

.book-item__details {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 4px;
  flex-shrink: 0;
}

.book-item__pages {
  font-size: 13px;
  color: #6b7280;

  span {
    font-weight: 600;
    color: #1a1a2e;
  }
}

.book-item__stars {
  display: flex;
  gap: 2px;
  font-size: 15px;
}

.book-item__star--filled {
  color: #f5a623;
}

.book-item__star--empty {
  color: #dde1ea;
}

</style>