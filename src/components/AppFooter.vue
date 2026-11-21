<template>
  <footer class="site-footer">
    <div class="container">
      <div class="footer-grid">
        <div class="footer-col">
          <div class="footer-logo">SNEAKER BOOM!</div>
          <p class="footer-tagline">
            Баскетбольные, беговые и повседневные кроссовки с супергеройским характером. Доставка по всему Казахстану!
          </p>
        </div>

        <div class="footer-col">
          <h3 class="footer-heading">Категории</h3>
          <ul class="footer-links">
            <li v-for="category in categories" :key="category">
              <button type="button" @click="handleCategoryClick(category)">
                {{ category }}
              </button>
            </li>
          </ul>
        </div>

        <div class="footer-col">
          <h3 class="footer-heading">Контакты</h3>
          <ul class="footer-contacts">
            <li>📍 г. Алматы, ул. Тастак, 1/1B</li>
            <li>📞 <a href="tel:+77479067052">+7 (747) 906-70-52</a></li>
            <li>✉️ <a href="mailto:info@sneakerboom.kz">info@sneakerboom.kz</a></li>
          </ul>
        </div>
      </div>

      <div class="footer-bottom">
        <span class="footer-copy">&copy; {{ currentYear }} SNEAKER BOOM! Все права защищены.</span>
        <span class="footer-badge">POW! КРОССОВКИ В НАЛИЧИИ!</span>
      </div>
    </div>
  </footer>
</template>

<script setup>
defineProps({
  categories: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['select-category'])
const currentYear = new Date().getFullYear()

const handleCategoryClick = (category) => {
  emit('select-category', category)
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>
