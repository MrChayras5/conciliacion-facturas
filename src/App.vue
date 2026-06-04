<template>
  <div class="layout">
    <aside class="sidebar">
      <h2>Conciliación</h2>

      <nav>
        <RouterLink to="/">Dashboard</RouterLink>
        <RouterLink to="/facturas">Facturas</RouterLink>
      </nav>
    </aside>

    <main class="content">
      <RouterView />
    </main>
  </div>
</template>

<style scoped>
.layout {
  display: flex;
  min-height: 100vh;
  font-family: Arial, sans-serif;
}

.sidebar {
  width: 240px;
  background: #1f2937;
  color: white;
  padding: 24px;
}

.sidebar h2 {
  margin-bottom: 32px;
}

.sidebar nav {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.sidebar a {
  color: #d1d5db;
  text-decoration: none;
  padding: 10px;
  border-radius: 6px;
}

.sidebar a.router-link-active {
  background: #374151;
  color: white;
}

.content {
  flex: 1;
  background: #f3f4f6;
  padding: 32px;
}
</style>
