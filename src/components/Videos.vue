<template>
  <div class="video-section-content">
    
    <!-- NUEVO: Contenedor para el estado y el botón de acción -->
    <div class="controls-bar">
      <p class="selection-status">Estado de la selección: **{{ seleccionEstado }}**</p>
      
      <!-- BOTÓN AÑADIDO: Solo visible si hay selecciones -->
      <button 
        v-if="selectedVideoIndices.size > 0"
        @click="clearSelection"
        class="btn-clear-selection"
      >
        Deseleccionar Todos ({{ selectedVideoIndices.size }})
      </button>
    </div>

    <div class="videos-grid">
      
      <div 
        v-for="(video, index) in vds.videos" 
        :key="index"
        class="video-item"
        :class="{ 'video-selected': selectedVideoIndices.has(index) }"
        @click="selectVideo(index)"
      >
        <div class="thumbnail-wrapper">
          <!-- La carga de la miniatura es correcta con video.url -->
          <img :src="video.url" :alt="video.title" class="video-thumbnail">
          <span class="duration-overlay">{{ video.duration }}</span>
        </div>
        
        <div class="video-info">
          <div class="text-content">
            <p class="video-title">{{ video.title }}</p>
            <p class="video-channel-details">CADI F1 C.A.</p>
            <p class="video-details">{{ formatViews(video.views) }} vistas · hace 3 días</p>
          </div>
        </div>
      </div>
      
    </div>
  </div>
</template>

<script setup>
import { reactive, ref, computed, onMounted } from 'vue';
// Requerimiento 2: Importar la data del JSON. AJUSTA LA RUTA SI ES NECESARIO (ej: '../assets/videos.json')
import videosData from '@/assets/videos.json'; 

// Requerimiento 2: Crear una variable reactiva "vds"
const vds = reactive(videosData);

// RASTREO DE MÚLTIPLES SELECCIONES: Un Set reactivo
const selectedVideoIndices = reactive(new Set()); 

// NUEVA FUNCIÓN: Limpia el Set de índices
const clearSelection = () => {
    selectedVideoIndices.clear();
};

// Función de utilidad para formatear vistas (e.g., 12345 -> 12.3 K)
const formatViews = (views) => {
  // Se asegura de que la lógica de formato sea consistente
  if (views > 999) {
    return (views / 1000).toFixed(1) + ' K';
  }
  return views.toString();
};

// Función para seleccionar/deseleccionar (AÑADIR O ELIMINAR del Set)
const selectVideo = (index) => {
  if (selectedVideoIndices.has(index)) {
    // Si ya está en la selección, lo elimina (deselecciona)
    selectedVideoIndices.delete(index);
  } else {
    // Si no está, lo agrega (selecciona)
    selectedVideoIndices.add(index);
  }
};

// Variable computada para el estado de la selección (Maneja 0, 1 o N selecciones)
const seleccionEstado = computed(() => {
  const count = selectedVideoIndices.size;
  
  if (count === 0) {
    return 'Ninguna selección activa';
  } else if (count === 1) {
    // Para obtener el índice único del Set
    const index = selectedVideoIndices.values().next().value;
    return `Selección activa: ${vds.videos[index].title}`;
  } else {
    return `${count} selecciones activas (${count} videos)`;
  }
});

// Requerimiento 5: Programar console.warn en onMounted
onMounted(() => {
  console.warn('El componente Videos.vue ha disparado el evento onMounted.');
});
</script>

<style scoped>
/* Estructura Principal y Controles */
.video-section-content {
    padding: 20px 24px; 
}

.controls-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    gap: 10px;
}

.selection-status {
    color: #444; 
    font-size: 1.1em;
    font-weight: bold; 
    margin: 0; 
}

/* Estilos del Botón Deseleccionar Todos */
.btn-clear-selection {
    background-color: #f00; 
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 500;
    transition: background-color 0.2s;
    flex-shrink: 0;
}
.btn-clear-selection:hover {
    background-color: #c00;
}

/* Cuadrícula de Videos */
.videos-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); 
    gap: 20px 16px; 
}

/* Ítem de Video */
.video-item {
    cursor: pointer;
    transition: all 0.2s; 
    border-radius: 8px;
    padding: 0; 
    box-sizing: border-box; 
}

/* Estilo de Selección Activa */
.video-selected {
    background-color: #a8e4a0; 
    padding: 8px;
    box-shadow: 0 0 0 2px green; 
}

/* Miniatura y Overlay */
.thumbnail-wrapper {
    position: relative;
    overflow: hidden;
    border-radius: 8px;
    aspect-ratio: 16 / 9; 
    margin-bottom: 0; /* Base */
}

.video-selected .thumbnail-wrapper {
    margin-bottom: 8px; /* Ajuste para el padding del item seleccionado */
}

.video-thumbnail {
    width: 100%;
    height: auto;
    display: block;
}

.duration-overlay {
    position: absolute;
    bottom: 8px;
    right: 8px;
    background-color: rgba(0, 0, 0, 0.8); 
    color: white;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 0.75em;
    font-weight: 500;
}

/* Información de Texto */
.video-info {
    padding-top: 12px; /* Base */
}

.video-selected .video-info {
    padding-top: 0; /* Ajuste para el item seleccionado */
}

.video-title {
    font-weight: 500;
    font-size: 1em;
    line-height: 1.4;
    margin: 0 0 4px 0; 
    height: 2.8em; 
    overflow: hidden;
    color: #030303; 
}

.video-channel-details,
.video-details {
    color: #606060;
    font-size: 0.9em;
    margin: 0; 
}
</style>
