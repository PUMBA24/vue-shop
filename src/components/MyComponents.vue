<template>
  <div class="product-card">
    <button
      type="button"
      class="product-preview"
      :aria-label="`Быстрый просмотр: ${title}`"
      @click="$emit('preview', product)"
    >
      <img :src="src" :alt="title" class="product-image" />
      <span class="preview-label">Быстрый просмотр</span>
    </button>
    <h2 class="product-title">Кроссовки: {{ title }}</h2>
    <p class="product-description">Описание: {{ description }}</p>
    <button
      class="product-buy-button"
      @click="$emit('buy', product)"
    >
      Купить {{ formattedPrice }} ₸
    </button>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  id: Number,
  src: String,
  title: String,
  price: Number,
  description: String,
  category: String
})

defineEmits(['preview', 'buy'])

const product = computed(() => ({
  id: props.id,
  src: props.src,
  title: props.title,
  price: props.price,
  description: props.description,
  category: props.category
}))

const formattedPrice = computed(() => props.price.toLocaleString('ru-RU'))
</script>