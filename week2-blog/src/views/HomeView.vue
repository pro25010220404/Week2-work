<script setup>
import { inject, computed } from 'vue'
import ArticleCard from '@/components/ArticleCard.vue'
import Pagination from '@/components/Pagination.vue'
import { articles } from '@/data/articles.js'

const pagination = inject('pagination', { currentPage: { value: 1 }, pageSize: 5 })

const paginatedArticles = computed(() => {
  const start = (pagination.currentPage.value - 1) * pagination.pageSize
  const end = start + pagination.pageSize
  return articles.slice(start, end)
})
</script>

<template>
  <div class="home-view">
    <!-- 文章列表 -->
    <section class="article-section">
      <h2 class="section-title">最新文章</h2>
      <div class="article-list">
        <ArticleCard
          v-for="article in paginatedArticles"
          :key="article.id"
          :article="article"
        />
      </div>
    </section>

    <!-- 分页组件 -->
    <section class="pagination-section">
      <Pagination
        :total="articles.length"
        :page-size="pagination.pageSize"
        v-model="pagination.currentPage.value"
      />
    </section>
  </div>
</template>

<style scoped>
.home-view {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.section-title {
  margin-bottom: var(--spacing-md);
}

.article-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}
</style>
