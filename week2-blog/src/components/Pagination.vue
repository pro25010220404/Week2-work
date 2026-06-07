<script setup>
import { ref, computed, watch } from 'vue'

const props = defineProps({
  total: {
    type: Number,
    default: 0,
  },
  pageSize: {
    type: Number,
    default: 5,
  },
  modelValue: {
    type: Number,
    default: 1,
  },
})

const emit = defineEmits(['update:modelValue'])

const currentPage = ref(props.modelValue)

watch(() => props.modelValue, (val) => {
  currentPage.value = val
})

const totalPages = computed(() => {
  return Math.max(1, Math.ceil(props.total / props.pageSize))
})

const pages = computed(() => {
  const result = []
  const maxVisible = 7
  let start = Math.max(1, currentPage.value - Math.floor(maxVisible / 2))
  let end = Math.min(totalPages.value, start + maxVisible - 1)

  if (end - start + 1 < maxVisible) {
    start = Math.max(1, end - maxVisible + 1)
  }

  for (let i = start; i <= end; i++) {
    result.push(i)
  }
  return result
})

const hasPrev = computed(() => currentPage.value > 1)
const hasNext = computed(() => currentPage.value < totalPages.value)

const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value && page !== currentPage.value) {
    currentPage.value = page
    emit('update:modelValue', page)
  }
}

const prevPage = () => {
  if (hasPrev.value) {
    currentPage.value--
    emit('update:modelValue', currentPage.value)
  }
}

const nextPage = () => {
  if (hasNext.value) {
    currentPage.value++
    emit('update:modelValue', currentPage.value)
  }
}
</script>

<template>
  <nav class="pagination" role="navigation" aria-label="分页导航">
    <button
      class="pagination__btn pagination__btn--prev"
      :disabled="!hasPrev"
      @click="prevPage"
      aria-label="上一页"
    >
      <svg class="pagination__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M15 19l-7-7 7-7" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </button>

    <ul class="pagination__list">
      <li v-if="pages[0] > 1" class="pagination__item">
        <button class="pagination__link" @click="goToPage(1)">1</button>
      </li>
      <li v-if="pages[0] > 2" class="pagination__item">
        <span class="pagination__ellipsis">...</span>
      </li>

      <li
        v-for="page in pages"
        :key="page"
        class="pagination__item"
      >
        <button
          class="pagination__link"
          :class="{ 'pagination__link--active': page === currentPage }"
          @click="goToPage(page)"
          :aria-current="page === currentPage ? 'page' : undefined"
        >
          {{ page }}
        </button>
      </li>

      <li v-if="pages[pages.length - 1] < totalPages - 1" class="pagination__item">
        <span class="pagination__ellipsis">...</span>
      </li>
      <li v-if="pages[pages.length - 1] < totalPages" class="pagination__item">
        <button class="pagination__link" @click="goToPage(totalPages)">{{ totalPages }}</button>
      </li>
    </ul>

    <button
      class="pagination__btn pagination__btn--next"
      :disabled="!hasNext"
      @click="nextPage"
      aria-label="下一页"
    >
      <svg class="pagination__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M9 5l7 7-7 7" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </button>
  </nav>
</template>

<style scoped>
.pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-xs);
  padding: var(--spacing-md);
  background-color: var(--color-bg-white);
  border: 1px solid var(--color-border);
  border-radius: var(--border-radius);
}

.pagination__btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  padding: 0;
  border: 1px solid var(--color-border);
  border-radius: var(--border-radius-sm);
  background-color: var(--color-bg-white);
  color: var(--color-text-secondary);
  cursor: pointer;
  transition: all 0.2s ease;
}

.pagination__btn:hover:not(:disabled) {
  border-color: var(--color-primary);
  color: var(--color-primary);
  background-color: rgba(var(--color-primary-rgb), 0.05);
}

.pagination__btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.pagination__icon {
  width: 16px;
  height: 16px;
}

.pagination__list {
  display: flex;
  align-items: center;
  gap: 4px;
  margin: 0;
  padding: 0;
  list-style: none;
}

.pagination__item {
  display: flex;
  align-items: center;
}

.pagination__link {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 36px;
  height: 36px;
  padding: 0 var(--spacing-sm);
  border: 1px solid transparent;
  border-radius: var(--border-radius-sm);
  background: transparent;
  font-size: var(--font-size-sm);
  font-weight: 500;
  color: var(--color-text-secondary);
  cursor: pointer;
  transition: all 0.2s ease;
}

.pagination__link:hover {
  color: var(--color-primary);
  background-color: rgba(var(--color-primary-rgb), 0.05);
}

.pagination__link--active {
  border-color: var(--color-primary);
  background-color: var(--color-primary);
  color: #fff;
}

.pagination__link--active:hover {
  background-color: var(--color-primary);
  color: #fff;
}

.pagination__ellipsis {
  display: flex;
  align-items: center;
  padding: 0 var(--spacing-xs);
  color: var(--color-text-secondary);
  font-size: var(--font-size-sm);
}
</style>
