<template>
  <div class="home-view">
    <!-- 成员3：文章列表前 3 篇 -->
    <section class="article-section">
      <h2 class="section-title">最新文章</h2>
      <div class="article-placeholder">
        <p class="layout-placeholder__hint">成员3：文章卡片 1 ~ 3</p>
      </div>
    </section>

    <!-- 成员4：文章列表后 2 篇 + 分页 -->
    <section class="article-section">
      <div class="article-placeholder">
        <p class="layout-placeholder__hint">成员4：文章卡片 4 ~ 5</p>
      </div>
      <div class="pagination-placeholder">
        <p class="layout-placeholder__hint text-secondary">成员4：分页按钮</p>
      </div>
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

.article-placeholder,
.pagination-placeholder {
  padding: var(--spacing-lg);
  background-color: var(--color-bg-white);
  border: 1px dashed var(--color-border);
  border-radius: var(--border-radius);
  text-align: center;
}

.pagination-placeholder {
  margin-top: var(--spacing-md);
}

.layout-placeholder__hint {
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  margin-bottom: 0;
}
</style>
