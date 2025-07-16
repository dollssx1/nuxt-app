<script setup lang="ts">
const input1 = ref('')
</script>

<template>
  <div>
    <header>
      <nav class="navbar">
        <div class="nav-container">
          <NuxtLink to="/" class="nav-logo">
            <AppLogo icon-only />
          </NuxtLink>
          <BaseInput  required size="medium" v-model="input1" :show-search-icon="true" placeholder="검색"></BaseInput>
          <ul class="nav-menu">
            <li class="nav-item">
              <NuxtLink to="/" class="nav-link">Home</NuxtLink>
            </li>
            <li class="nav-item">
              <NuxtLink to="/about" class="nav-link">About</NuxtLink>
            </li>
          </ul>
        </div>
      </nav>
    </header>

    <main class="main-content">
      <slot />
    </main>

    <footer class="footer">
      <div class="footer-container">
        <p>&copy; 2025 My App. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<style lang="scss" scoped>
.navbar {
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 1rem 0;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: #333;
  text-decoration: none;
}

.nav-menu {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 2rem;
}

.nav-link {
  color: #666;
  text-decoration: none;
  transition: color 0.3s;

  &:hover,
  &.router-link-active {
    color: #007bff;
  }
}

.main-content {
  min-height: calc(100vh - 140px);
  padding: 2rem 0;
}

.footer {
  background-color: #f8f9fa;
  padding: 2rem 0;
  margin-top: auto;
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
  text-align: center;
  color: #666;
}
</style>
