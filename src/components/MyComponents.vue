<template>
  <div class="product-card">
    <img :src="src" :alt="title" class="product-image" />
    <h2 class="product-title">Кроссовки: {{ title }}</h2>
    <p class="product-description">Описание: {{ description }}</p>
    <button
      class="product-buy-button"
    >
      Купить {{ formattedPrice }} ₸
    </button>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  src: String,
  title: String,
  price: Number,
  description: String
})

const formattedPrice = computed(() => props.price.toLocaleString('ru-RU'))
</script>