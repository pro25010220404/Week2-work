<script setup>
defineProps({
  article: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <article class="article-card">
    <header class="article-card__header">
      <a href="#" class="article-card__title">{{ article.title }}</a>
      <div class="article-card__meta">
        <time class="article-card__date" :datetime="article.date">{{ article.date }}</time>
        <span class="article-card__divider">·</span>
        <a href="#" class="article-card__category">{{ article.category }}</a>
        <span class="article-card__divider">·</span>
        <span class="article-card__read-time">{{ article.readTime }}</span>
      </div>
    </header>

    <p class="article-card__summary">{{ article.summary }}</p>

    <footer class="article-card__footer">
      <div class="article-card__tags">
        <a
          v-for="tag in article.tags"
          :key="tag"
          href="#"
          class="article-card__tag"
        >
          # {{ tag }}
        </a>
      </div>
      <span class="article-card__views">{{ article.views }} 阅读</span>
    </footer>
  </article>
</template>

<style scoped>
.article-card {
  padding: var(--spacing-lg);
  background-color: var(--color-bg-white);
  border: 1px solid var(--color-border);
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  transition: box-shadow 0.2s ease, transform 0.2s ease;
}

.article-card:hover {
  box-shadow: 0 4px 20px rgba(60, 56, 53, 0.1);
  transform: translateY(-2px);
}

.article-card__header {
  margin-bottom: var(--spacing-sm);
}

.article-card__title {
  display: block;
  font-size: var(--font-size-lg);
  font-weight: 600;
  line-height: 1.4;
  color: var(--color-text);
  margin-bottom: var(--spacing-xs);
  transition: color 0.2s ease;
}

.article-card__title:hover {
  color: var(--color-primary);
}

.article-card__meta {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 6px;
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
}

.article-card__divider {
  color: var(--color-border);
}

.article-card__category {
  color: var(--color-accent);
}

.article-card__category:hover {
  color: var(--color-primary);
}

.article-card__summary {
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  line-height: 1.8;
  margin-bottom: var(--spacing-md);
}

.article-card__footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--spacing-sm);
  flex-wrap: wrap;
}

.article-card__tags {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-xs);
}

.article-card__tag {
  display: inline-flex;
  align-items: center;
  padding: 4px 10px;
  font-size: 0.8125rem;
  color: var(--color-accent);
  background-color: #f1f6f2;
  border: 1px solid #d8e5db;
  border-radius: 999px;
  transition: all 0.2s ease;
}

.article-card__tag:hover {
  color: #fff;
  background-color: var(--color-accent);
  border-color: var(--color-accent);
}

.article-card__views {
  flex-shrink: 0;
  font-size: 0.8125rem;
  color: var(--color-text-secondary);
}
</style>
