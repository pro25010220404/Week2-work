<script setup>
import { ref } from 'vue'
import AppFooter from '@/components/AppFooter.vue'

const hotPosts = [
  { title: 'Vue 3 组合式 API 入门', views: '1.2k' },
  { title: 'Vite 搭建博客项目实践', views: '986' },
  { title: '前端页面响应式布局技巧', views: '854' },
]

const categories = [
  { name: '前端开发', count: 8 },
  { name: 'Vue 学习', count: 5 },
  { name: '项目实战', count: 3 },
  { name: '随笔记录', count: 2 },
]

const tags = ['Vue', 'Vite', 'JavaScript', 'CSS', '响应式', '组件化', '博客', '前端']

const friendLinks = [
  { name: 'Vue 官方文档', url: 'https://cn.vuejs.org/' },
  { name: 'Vite 官方文档', url: 'https://cn.vite.dev/' },
  { name: 'Element Plus', url: 'https://element-plus.org/zh-CN/' },
]

const navItems = [
  { name: '首页', href: '#home' },
  { name: '文章', href: '#articles' },
  { name: '关于', href: '#about' },
]

const searchQuery = ref('')
</script>

<template>
  <div class="main-layout">
    <header class="layout-header">
      <div class="container layout-header__inner">
        <div class="header-brand">
          <img class="header-brand__logo" src="/博客logo.png" alt="博客 logo" />
          <span class="header-brand__label">Week2 Blog</span>
        </div>

        <nav class="layout-header__nav" aria-label="主导航">
          <a v-for="item in navItems" :key="item.name" :href="item.href" class="nav-link">
            {{ item.name }}
          </a>
        </nav>

        <div class="layout-header__search">
          <input
            v-model="searchQuery"
            type="search"
            class="search-input"
            placeholder="搜索文章、标签、关键词"
            aria-label="搜索文章"
          />
        </div>
      </div>
    </header>

    <div class="layout-main">
      <main class="layout-content">
        <router-view />
      </main>

      <aside class="layout-sidebar">
        <slot name="sidebar">
          <section class="sidebar-card sidebar-card--highlight">
            <h3 class="sidebar-card__title">站点信息</h3>
            <p class="sidebar-card__desc">
              这是一个简洁的博客首页示例，包含文章区、侧边栏和响应式布局，适合作为课程作业展示页面。
            </p>
            <div class="site-stats">
              <div class="site-stats__item">
                <strong>5</strong>
                <span>文章</span>
              </div>
              <div class="site-stats__item">
                <strong>4</strong>
                <span>分类</span>
              </div>
              <div class="site-stats__item">
                <strong>8</strong>
                <span>标签</span>
              </div>
            </div>
          </section>

          <section class="sidebar-card">
            <h3 class="sidebar-card__title">热门文章</h3>
            <ul class="sidebar-list">
              <li v-for="post in hotPosts" :key="post.title" class="sidebar-list__item">
                <a href="#">{{ post.title }}</a>
                <span class="sidebar-list__meta">{{ post.views }}</span>
              </li>
            </ul>
          </section>

          <section class="sidebar-card">
            <h3 class="sidebar-card__title">分类列表</h3>
            <ul class="category-list">
              <li v-for="category in categories" :key="category.name" class="category-list__item">
                <a href="#">{{ category.name }}</a>
                <span class="category-list__count">{{ category.count }}</span>
              </li>
            </ul>
          </section>

          <section class="sidebar-card">
            <h3 class="sidebar-card__title">标签云</h3>
            <div class="tag-cloud">
              <a v-for="tag in tags" :key="tag" href="#" class="tag-cloud__item"># {{ tag }}</a>
            </div>
          </section>

          <section class="sidebar-card">
            <h3 class="sidebar-card__title">关于 / 友链</h3>
            <p class="sidebar-card__desc">
              成员5负责右侧栏与移动端适配，当前展示常见博客模块：站点简介、热门文章、分类、标签与友链。
            </p>
            <ul class="friend-links">
              <li v-for="link in friendLinks" :key="link.name">
                <a :href="link.url" target="_blank" rel="noopener">{{ link.name }}</a>
              </li>
            </ul>
          </section>
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
  position:fixed;
  top:0;
  left:0;
  width:100%;
  z-index: 1000;
}

.layout-header__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  gap: var(--spacing-md);
}

.header-brand {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
}

.header-brand__logo {
  width: 55px;
  height: 55px;
  object-fit: contain;
  border-radius: 8px;
  background-color: #fff;
}

.header-brand__label {
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
}

.layout-header__nav {
  display: flex;
  align-items: center;
  gap: var(--spacing-lg);
}

.nav-link {
  font-size: var(--font-size-base);
  color: var(--color-text);
  position: relative;
  padding: 4px 0;
  transition: color 0.2s ease;
}

.nav-link:hover,
.nav-link:focus-visible {
  color: var(--color-primary);
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -2px;
  width: 0;
  height: 2px;
  background-color: var(--color-primary);
  transition: width 0.2s ease;
}

.nav-link:hover::after,
.nav-link:focus-visible::after {
  width: 100%;
}

.nav-link.active {
  color: var(--color-primary);
  font-weight: 600;
}

.layout-header__search {
  display: flex;
  align-items: center;
}

.search-input {
  width: 220px;
  padding: 8px 12px 8px 38px;
  font-size: var(--font-size-sm);
  color: var(--color-text);
  border: 1px solid var(--color-border);
  border-radius: 999px;
  background-color: var(--color-bg);
  background-image: url(../../public/search.svg);
  background-repeat: no-repeat;
  background-position: 12px center;
  background-size: 18px;
  transition: border-color 0.2s ease, box-shadow 0.2s ease, transform 0.2s ease;
}

.search-input:hover {
  transform: translateY(-1px);
}

.search-input:focus {
  border-color: var(--color-primary);
  box-shadow: 0 0 0 4px rgba(158, 128, 96, 0.08);
}

@media (max-width: 880px) {
  .layout-header__inner {
    flex-wrap: wrap;
    justify-content: space-between;
    gap: var(--spacing-sm);
  }

  .layout-header__nav {
    order: 3;
    width: 100%;
    justify-content: center;
    flex-wrap: wrap;
    gap: var(--spacing-md);
    padding: var(--spacing-sm) 0;
  }

  .layout-header__search {
    order: 2;
    width: 100%;
    justify-content: center;
  }

  .search-input {
    width: min(100%, 240px);
  }
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

.sidebar-card--highlight {
  background: linear-gradient(180deg, #fffcf8 0%, #f8f1e8 100%);
}

.sidebar-card__title {
  font-size: var(--font-size-base);
  margin-bottom: var(--spacing-sm);
  padding-bottom: var(--spacing-sm);
  border-bottom: 1px solid var(--color-border);
}

.sidebar-card__desc {
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  line-height: 1.8;
}

.site-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--spacing-sm);
  margin-top: var(--spacing-md);
}

.site-stats__item {
  padding: var(--spacing-sm);
  text-align: center;
  background-color: rgba(255, 255, 255, 0.75);
  border: 1px solid var(--color-border);
  border-radius: var(--border-radius);
}

.site-stats__item strong {
  display: block;
  font-size: 1.125rem;
  color: var(--color-primary);
}

.site-stats__item span {
  font-size: 0.8125rem;
  color: var(--color-text-secondary);
}

.sidebar-list,
.category-list,
.friend-links {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-sm);
}

.sidebar-list__item,
.category-list__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--spacing-sm);
}

.sidebar-list__meta,
.category-list__count {
  flex-shrink: 0;
  font-size: 0.8125rem;
  color: var(--color-text-secondary);
  background-color: var(--color-bg);
  padding: 2px 8px;
  border-radius: 999px;
}

.tag-cloud {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-sm);
}

.tag-cloud__item {
  display: inline-flex;
  align-items: center;
  padding: 6px 12px;
  font-size: 0.875rem;
  color: var(--color-accent);
  background-color: #f1f6f2;
  border: 1px solid #d8e5db;
  border-radius: 999px;
  transition: all 0.2s ease;
}

.tag-cloud__item:hover {
  color: #fff;
  background-color: var(--color-accent);
  border-color: var(--color-accent);
}

.friend-links a,
.sidebar-list a,
.category-list a {
  display: inline-block;
  line-height: 1.6;
}

@media (max-width: 1024px) {
  .layout-placeholder--header {
    gap: var(--spacing-sm);
  }

  .layout-placeholder__hint {
    text-align: right;
  }
}

@media (max-width: 768px) {
  .layout-header {
    height: auto;
  }

  .layout-header__inner {
    padding: var(--spacing-md) 0;
  }

  .layout-placeholder,
  .layout-placeholder--header {
    flex-direction: column;
    align-items: flex-start;
  }

  .layout-placeholder__hint {
    text-align: left;
  }

  .site-stats {
    grid-template-columns: 1fr;
  }
}
</style>
