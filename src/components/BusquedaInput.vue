<template>
  <div class="search-wrapper">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="search-icon">
      <circle cx="11" cy="11" r="8"></circle>
      <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
    </svg>
    
    <!-- Input con v-model :D -->
    <input 
      type="text" 
      placeholder="Buscar"
      v-model="busqueda"
    />
  </div>
</template>

<script setup>
const busqueda = defineModel('busqueda');
</script>

<style scoped>
.search-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  width: 240px;
}

.search-icon {
  position: absolute;
  left: 12px;
  color: #606060;
}

input {
  width: 100%;
  padding: 8px 12px 8px 40px; 
  border: 1px solid transparent;
  border-bottom-color: #ccc;
  background-color: transparent;
  font-size: 14px;
  transition: all 0.2s ease;
}

input:focus {
  outline: none;
  border-bottom-color: #030303;
  background-color: #f0f0f0;
}
</style>
