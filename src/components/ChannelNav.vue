<template>
  <div class="channel-nav-container">
    <button class="arrow-btn">&lt;</button>
    <ul class="nav-list">
      <li><a href="#" class="active">VIDEOS</a></li>
      <li><a href="#">SHORTS</a></li>
      <li><a href="#">EN DIRECTO</a></li>
      <li><a href="#">LISTAS</a></li>
      <li><a href="#">COMUNIDAD</a></li>
      <li><a href="#">CANALES</a></li>
      <li><a href="#">INFORMACIÓN</a></li>
    </ul>
    <button class="arrow-btn">&gt;</button>
  </div>
</template>

<script setup>
// No nos adelantemos tanto :p
</script>

<style scoped>
.channel-nav-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 15px;
  border-bottom: 1px solid #ddd;
  margin-top: 20px;
}

.nav-list {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  overflow-x: auto;
  scrollbar-width: none;
}
.nav-list::-webkit-scrollbar { display: none; }

.nav-list li a {
  display: block;
  padding: 12px 16px;
  text-decoration: none;
  color: #606060;
  font-weight: 500;
  font-size: 14px;
  text-transform: uppercase;
  white-space: nowrap;
  border-bottom: 3px solid transparent;
}

.nav-list li a.active,
.nav-list li a:hover {
  color: #030303;
  border-bottom-color: #030303;
}

.arrow-btn {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 24px;
  color: #606060;
  padding: 0 10px;
}
</style>
