<script setup>
import { ref, computed, onMounted, onUnmounted, watch } from 'vue'
import MyComponents from './components/MyComponents.vue'
import AppFooter from './components/AppFooter.vue'

const images = [
  'https://resources.cdn-kaspi.kz/img/m/p/p1d/pe1/141771539.jpeg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/p14/p5c/126585440.jpg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/p93/pa3/40391515.jpeg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/p1e/p99/75524319.jpeg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/pac/p0b/104880511.jpg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/p2f/p67/19868767.jpg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/p46/p05/204042180.jpg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/pe0/pad/197236957.jpg?format=gallery-medium',
  'https://resources.cdn-kaspi.kz/img/m/p/p84/pc2/197235631.jpg?format=gallery-medium',
]

const products = [
  {
    id: 1,
    src: images[0],
    category: 'Баскетбольные',
    title: 'Nike HyperSet2',
    price: 35000,
    description:
      'Nike Air Zoom HyperSet 2 - баскетбольные кроссовки средней высоты. Модель пришла на смену легендарных Nike Hyperdunk X. Мы видим такую же подошву с двумя подушками Air Zoom в носовой и пяточной области, для уверенных рывков и отличного гашения ударов. Зарекомендовавший себя волнистый рисунок подошвы, так же оставили без изменений. Особенность баскетбольных кроссовок Nike Air Zoom HyperSet 2, это ярко выраженная боковая поддержка в виде пластиковой вставки в форме лого Nike. Верх выполнен из плотного ТПУ, с дышащей сеткой в носовой части. Получились максимально универсальные баскетбольные кроссовки как для мужчин, так и для женщин. Уличная крошка или паркет зала, кроссовки будут себя чувствовать уверенно на любой поверхности.',
  },
  {
    id: 2,
    category: 'Беговые',
    src: images[1],
    title: 'Puma Pulse Pro Running Shoes Unisex бежевый',
    price: 47994,
    description:
      'Пристегните ремень безопасности и почувствуйте пульс с новейшей моделью PUMA с высокой производительностью. Оснащены технологией PROFOAM для отзывчивой амортизации, PROTREAD для сцепления с различными поверхностями и TPU-пятой для улучшенной поддержки. Будьте готовы покорять каждый забег с ловкостью и стилем.',
  },
  {
    id: 3,
    src: images[2],
    category: 'Повседневные',
    title: 'Reebok бежевый',
    price: 200000,
    description:
      'Кроссовки Reebok Classic Leather — это идеальное сочетание стиля и комфорта для повседневного использования. Их натуральные материалы и анатомическая подошва обеспечивают отличную поддержку и удобство на протяжении всего дня.',
  },
  {id: 4,
    src: images[3],
    category: 'Баскетбольные',
    title: 'Rare',
    price: 11500,
    description:
      'Изготовлены из чистой ткани, что делает их лёгкими, дышащими и приятными к ноге. Прочная подошва обеспечивает отличное сцепление и амортизацию, снижая нагрузку на суставы при прыжках и резких поворотах.',
  },
  {id: 5,
    src: images[4],
    category: 'Беговые',
    title: 'LI-NING SOFT GO 3',
    price: 45000,
    description:
      'Мужские демисезонные кроссовки AGLW001 из повседневной серии SOFT GO 3 предназначены для комфортной носки в городских условиях. Модель ориентирована на повседневное использование и спокойный ритм активности. Верх выполнен из текстиля с элементами термопластичного полиуретана (TPU). Такое сочетание обеспечивает лёгкость, хорошую фиксацию стопы и устойчивость формы при ходьбе. Материал практичен в эксплуатации и подходит для демисезонного периода. Подошва состоит из резины и промежуточного слоя Phylon. Данная конструкция обеспечивает амортизацию, комфорт при длительной ходьбе и устойчивость на различных поверхностях. Кроссовки рассчитаны на регулярную носку и подходят для повседневных задач.',
  },
  {id: 6,
  src: images[5],
  category: 'Повседневные',
  title: 'Nike SB Force белый',
  price: 29000,
  description:
    'Кроссовки Nike SB FORCE — это универсальная модель для тех, кто ценит комфорт и стиль в повседневной жизни и во время занятий спортом. '
  },
  {id: 7,
  src: images[6],
  category: 'Баскетбольные',
  title: 'Nike Air Max SNDR',
  price: 90230,
  description:
    'Женские кроссовки Nike Air Max SNDR. Модель надевается без шнуровки: верх затягивается скрытой системой, сверху и сзади петли-пуллеры — обуться можно одним движением. По борту идут рельефные перфорированные накладки, они держат форму и вентилируют стопу. В подошве видимая воздушная камера Air гасит удар при шаге, агрессивный протектор цепко держит на мокром асфальте. Винно-бордовая гамма с бирюзовым градиентом на мыске и бирюзовым Swoosh.',
  },
  {id: 8,
  src: images[7],
  category: 'Беговые',
  title: ' Nike Vomero Plus',
  price: 73050,
  description:
    'Женские беговые кроссовки Nike Vomero Plus с максимальной амортизацией. В подошве толстый слой пены ZoomX возвращает энергию на отталкивании и гасит удар при приземлении — ноги не устают на длинной дистанции. Инженерная сетка верха с рельефным рисунком вентилирует стопу и тянется по подъёму. Петля на пятке помогает быстро обуться. Розовый верх с фиолетово-оранжевой подошвой ZoomX.'
  },
  {id: 9,
  src: images[8],
  category: 'Повседневные',
  title: ' Nike Jordan CMFT Era белый',
  price: 52530,
  description:
    'Детские кроссовки Jordan CMFT Era — модель для города, а не для площадки. Верх комбинирует сетку и замшевые накладки: сетка вентилирует стопу, замша держит форму на мыске и пятке. Толстая промежуточная подошва гасит удар при шаге, скошенная пятка облегчает перекат. Петля на заднике помогает быстро обуться. Белый верх с тёмно-бирюзовой замшей и голубым Swoosh, логотип Jumpman на боковой части.',
  },

]

const activeCategory = ref('Все')
const searchQuery = ref('')
const selectedProduct = ref(null)
const quickViewQuantity = ref(1)
const cartItems = ref([])
const cartOpen = ref(false)
const cartMessage = ref('')
const cartCount = computed(() =>
  cartItems.value.reduce((sum, item) => sum + item.quantity, 0)
)
const cartTotal = computed(() =>
  cartItems.value.reduce((sum, item) => sum + item.product.price * item.quantity, 0)
)

const categories = computed(() => {
  const uniqueCategories = new Set(products.map((product) => product.category))
  return ['Все', ...uniqueCategories]
})

const filteredProducts = computed(() => {
  const query = searchQuery.value.trim().toLowerCase()
  return products.filter((product) => {
    const matchesCategory =
      activeCategory.value === 'Все' || product.category === activeCategory.value
    const matchesSearch = product.title.toLowerCase().includes(query)
    return matchesCategory && matchesSearch
  })
})

const setActiveCategory = (category) => {
  activeCategory.value = category
}

const resetFilters = () => {
  activeCategory.value = 'Все'
  searchQuery.value = ''
}

const openQuickView = (product) => {
  selectedProduct.value = product
  quickViewQuantity.value = 1
}

const closeQuickView = () => {
  selectedProduct.value = null
}

const addToCart = (product, quantity = 1) => {
  const existingItem = cartItems.value.find((item) => item.product.id === product.id)
  if (existingItem) {
    existingItem.quantity += quantity
  } else {
    cartItems.value.push({ product, quantity })
  }
  cartMessage.value = `${product.title} добавлен в корзину`
  window.setTimeout(() => {
    cartMessage.value = ''
  }, 2600)
}

const changeCartQuantity = (productId, change) => {
  const item = cartItems.value.find((cartItem) => cartItem.product.id === productId)
  if (!item) return
  item.quantity += change
  if (item.quantity < 1) removeFromCart(productId)
}

const removeFromCart = (productId) => {
  cartItems.value = cartItems.value.filter((item) => item.product.id !== productId)
}

const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeQuickView()
    cartOpen.value = false
  }
}

watch([selectedProduct, cartOpen], ([product, isCartOpen]) => {
  document.body.style.overflow = product || isCartOpen ? 'hidden' : ''
})

onMounted(() => window.addEventListener('keydown', handleKeydown))
onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
  document.body.style.overflow = ''
})
</script>

<template>
  <main class="app">
    <div class="container">
      <header class="page-header-row">
        <h1 class="page-header">
          Наши продукты
        </h1>
        <button
          type="button"
          class="cart-counter"
          :aria-label="`Открыть корзину, товаров: ${cartCount}`"
          @click="cartOpen = true"
        >
          Корзина <span>{{ cartCount }}</span>
        </button>
      </header>

      <div class="filters">
        <div class="category-list">
          <button
            v-for="category in categories"
            :key="category"
            @click="setActiveCategory(category)"
            :class="{ 'is-active': activeCategory === category }"
            class="category-button"
          >
            {{ category }}
          </button>
        </div>

        <input
          v-model="searchQuery"
          type="text"
          placeholder="Поиск по названию..."
          class="search-input"
        />
      </div>

      <div
        v-if="filteredProducts.length > 0"
        class="product-grid"
      >
        <MyComponents
          v-for="p in filteredProducts"
          :key="p.id"
          v-bind="p"
          @preview="openQuickView"
          @buy="addToCart"
        />
      </div>

      <div
        v-else
        class="empty-state"
      >
        <p class="empty-state-message">Товары не найдены</p>
        <button
          @click="resetFilters"
          class="reset-button"
        >
          Сбросить фильтры
        </button>
      </div>
    </div>

    <Teleport to="body">
      <div
        v-if="selectedProduct"
        class="quick-view-backdrop"
        role="presentation"
        @mousedown.self="closeQuickView"
      >
        <section
          class="quick-view"
          role="dialog"
          aria-modal="true"
          :aria-label="`Быстрый просмотр ${selectedProduct.title}`"
        >
          <button
            type="button"
            class="quick-view-close"
            aria-label="Закрыть"
            @click="closeQuickView"
          >
            ×
          </button>

          <div class="quick-view-image-wrap">
            <img
              :src="selectedProduct.src"
              :alt="selectedProduct.title"
              class="quick-view-image"
            />
          </div>

          <div class="quick-view-content">
            <span class="quick-view-category">{{ selectedProduct.category }}</span>
            <h2 class="quick-view-title">{{ selectedProduct.title }}</h2>
            <p class="quick-view-description">{{ selectedProduct.description }}</p>

            <div class="quick-view-actions">
              <strong class="quick-view-price">
                {{ selectedProduct.price.toLocaleString('ru-RU') }} ₸
              </strong>
              <div class="quantity-picker" aria-label="Количество">
                <button
                  type="button"
                  aria-label="Уменьшить количество"
                  @click="quickViewQuantity = Math.max(1, quickViewQuantity - 1)"
                >
                  −
                </button>
                <span>{{ quickViewQuantity }}</span>
                <button
                  type="button"
                  aria-label="Увеличить количество"
                  @click="quickViewQuantity += 1"
                >
                  +
                </button>
              </div>
              <button
                type="button"
                class="quick-view-buy"
                @click="addToCart(selectedProduct, quickViewQuantity); closeQuickView()"
              >
                В корзину
              </button>
            </div>
          </div>
        </section>
      </div>
    </Teleport>

    <Teleport to="body">
      <div
        v-if="cartOpen"
        class="cart-backdrop"
        role="presentation"
        @mousedown.self="cartOpen = false"
      >
        <aside class="cart-drawer" role="dialog" aria-modal="true" aria-label="Корзина">
          <header class="cart-drawer-header">
            <h2>Корзина</h2>
            <button
              type="button"
              class="cart-drawer-close"
              aria-label="Закрыть корзину"
              @click="cartOpen = false"
            >
              ×
            </button>
          </header>

          <div v-if="cartItems.length" class="cart-items">
            <article v-for="item in cartItems" :key="item.product.id" class="cart-item">
              <img :src="item.product.src" :alt="item.product.title" class="cart-item-image" />
              <div class="cart-item-info">
                <h3>{{ item.product.title }}</h3>
                <strong>{{ item.product.price.toLocaleString('ru-RU') }} ₸</strong>
                <div class="cart-item-controls">
                  <button
                    type="button"
                    :aria-label="`Уменьшить количество ${item.product.title}`"
                    @click="changeCartQuantity(item.product.id, -1)"
                  >
                    −
                  </button>
                  <span>{{ item.quantity }}</span>
                  <button
                    type="button"
                    :aria-label="`Увеличить количество ${item.product.title}`"
                    @click="changeCartQuantity(item.product.id, 1)"
                  >
                    +
                  </button>
                  <button
                    type="button"
                    class="cart-remove"
                    :aria-label="`Удалить ${item.product.title}`"
                    @click="removeFromCart(item.product.id)"
                  >
                    Удалить
                  </button>
                </div>
              </div>
            </article>
          </div>

          <div v-else class="cart-empty">
            <p>Корзина пуста</p>
            <button type="button" @click="cartOpen = false">Продолжить покупки</button>
          </div>

          <footer v-if="cartItems.length" class="cart-drawer-footer">
            <div>
              <span>Итого</span>
              <strong>{{ cartTotal.toLocaleString('ru-RU') }} ₸</strong>
            </div>
          </footer>
        </aside>
      </div>
    </Teleport>

    <div v-if="cartMessage" class="cart-toast" role="status">
      {{ cartMessage }}
    </div>
    <AppFooter
      :categories="categories"
      @select-category="setActiveCategory"
    />
  </main>
</template>


