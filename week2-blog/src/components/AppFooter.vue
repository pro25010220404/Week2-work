<template>
  <footer class="app-footer">
    <div class="container app-footer__inner">
      <p class="app-footer__copyright">© 2026 Week2 Blog. All rights reserved.</p>
      <p class="app-footer__contact text-secondary">
        联系：
        <a href="mailto:example@email.com">example@email.com</a>
        ·
        <a href="https://github.com" target="_blank" rel="noopener">GitHub</a>
      </p>
    </div>
  </footer>
</template>

<style scoped>
.app-footer {
  height: var(--footer-height);
  margin-top: auto;
  background-color: var(--color-bg-white);
  border-top: 1px solid var(--color-border);
}

.app-footer__inner {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-xs);
  height: 100%;
  text-align: center;
}

.app-footer__copyright {
  font-size: var(--font-size-sm);
  margin-bottom: 0;
}

.app-footer__contact {
  font-size: var(--font-size-sm);
  margin-bottom: 0;
}
</style>
