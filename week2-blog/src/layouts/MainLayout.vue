<script setup>
import AppFooter from '@/components/AppFooter.vue'
</script>

<template>
  <div class="main-layout">
    <header class="layout-header">
      <!-- 成员2：导航栏 Header / Nav -->
      <div class="container layout-header__inner">
        <slot name="header">
          <div class="layout-placeholder layout-placeholder--header">
            <span class="layout-placeholder__logo">Logo</span>
            <span class="layout-placeholder__hint">成员2：导航栏（首页 / 文章 / 关于 / 搜索）</span>
          </div>
        </slot>
      </div>
    </header>

    <div class="layout-main">
      <main class="layout-content">
        <router-view />
      </main>

      <aside class="layout-sidebar">
        <!-- 成员5：侧边栏 Aside -->
        <slot name="sidebar">
          <div class="sidebar-card">
            <h3 class="sidebar-card__title">热门文章</h3>
            <p class="layout-placeholder__hint text-secondary">成员5：侧边栏内容</p>
          </div>
          <div class="sidebar-card">
            <h3 class="sidebar-card__title">分类列表</h3>
          </div>
          <div class="sidebar-card">
            <h3 class="sidebar-card__title">标签云</h3>
          </div>
          <div class="sidebar-card">
            <h3 class="sidebar-card__title">关于 / 链接</h3>
          </div>
        </slot>
      </aside>
    </div>

    <AppFooter />
  </div>
</template>

<style scoped>
.main-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.layout-header {
  height: var(--header-height);
  background-color: var(--color-bg-white);
  border-bottom: 1px solid var(--color-border);
  box-shadow: var(--box-shadow);
}

.layout-header__inner {
  display: flex;
  align-items: center;
  height: 100%;
}

.layout-placeholder {
  display: flex;
  align-items: center;
  gap: var(--spacing-md);
  width: 100%;
}

.layout-placeholder--header {
  justify-content: space-between;
}

.layout-placeholder__logo {
  font-size: var(--font-size-lg);
  font-weight: 600;
  color: var(--color-primary);
}

.layout-placeholder__hint {
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
}

.layout-sidebar {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.sidebar-card {
  padding: var(--spacing-md);
  background-color: var(--color-bg-white);
  border: 1px solid var(--color-border);
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
}

.sidebar-card__title {
  font-size: var(--font-size-base);
  margin-bottom: var(--spacing-sm);
  padding-bottom: var(--spacing-sm);
  border-bottom: 1px solid var(--color-border);
}
</style>
