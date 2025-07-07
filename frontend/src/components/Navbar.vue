<script setup lang="ts">

import {computed, ref} from "vue";

const isCollapsed = ref(false)
const isAdmin = ref(true);

const toggleCollapse = () => {
  isCollapsed.value = !isCollapsed.value
}

const allRoutes = [
  { path: '/', name: 'Home', icon: 'home' },
];

const filteredRoutes = computed(() => {
  return isAdmin.value
      ? allRoutes
      : allRoutes.filter(route => route.path === '/');
});


</script>

<template>
  <div class="navbar-container" :class="{ collapsed: isCollapsed }">
    <button class="toggle-btn" @click="toggleCollapse">
      {{ isCollapsed ? '☰' : '×' }}
    </button>

    <nav class="navbar">
      <RouterLink v-for="route in filteredRoutes" :key="route.path" :to="route.path" class="nav-link">
        <div class="icon-container">
          <img class="nav-icon" :src="'/' + route.icon + '.svg'" width="25" height="25" />
        </div>
        <div class="text-container">
          <span class="nav-text">{{ route.name }}</span>
        </div>
      </RouterLink>
    </nav>
  </div>
</template>


<style scoped>
.navbar-container {
  --navbar-width: 200px;
  --navbar-collapsed-width: 60px;
  --transition-duration: 0.3s;

  width: var(--navbar-width);
  height: 100vh;
  background-color: #2c3e50;
  color: white;
  transition: width var(--transition-duration) ease;
  flex-shrink: 0;
  overflow: hidden;
}

.navbar-container.collapsed {
  width: var(--navbar-collapsed-width);
}

.toggle-btn {
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
  margin-bottom: 1rem;
  padding: 0.5rem;
  align-self: flex-start;
  width: 100%;
  text-align: center;
}

.toggle-btn:hover {
  background-color: #34495e;
}

.navbar {
  display: flex;
  flex-direction: column;
  height: calc(100% - 50px);
  gap: 4px;
  padding: 0 8px;
}

.nav-link {
  color: white;
  text-decoration: none;
  display: flex;
  align-items: center;
  border-radius: 4px;
  padding: 8px;
  transition: background-color 0.2s;
  overflow: hidden;
}

.icon-container {
  width: 25px;
  height: 25px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
}

.text-container {
  overflow: hidden;
  margin-left: 12px;
  transition:
      opacity var(--transition-duration) ease,
      margin var(--transition-duration) ease;
}

.nav-text {
  white-space: nowrap;
  opacity: 1;
}

.navbar-container.collapsed .text-container {
  opacity: 0;
  margin-left: 0;
  width: 0;
}

.nav-link:hover {
  background-color: #34495e;
}

.nav-link.router-link-exact-active {
  background-color: #42b983;
  font-weight: bold;
}

.bottom {
  margin-top: auto;
  margin-bottom: 20px;
}

</style>