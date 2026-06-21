<script setup lang="ts">
defineProps<{
  rating: number
}>()
</script>

<template>
  <div class="book-item__stars">
    <span v-for="star in 5" :key="star" :class="star<=rating ? 'book-item__star--filled' : 'book-item__star--empty'">
    ★
    </span>
  </div>
</template>

<style scoped>

</style>