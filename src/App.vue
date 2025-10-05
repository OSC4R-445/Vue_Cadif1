<template>
  <div id="perfil-canal">
    
    <CanalBanner :imgBanner="Cliente.imgBanner" :imgLogo="Cliente.imgLogo" /> 

    <div class="perfil-info-container">
      
      <CanalInfo :Cliente="Cliente" :suscrito="suscrito" @update:suscrito="suscrito = $event" />

      <div class="nav-and-search-container">
        <ChannelNav />
        <BusquedaInput v-model:busqueda="busqueda" />
      </div>

    </div>

    <!-- El h1 de la búsqueda ahora se renderiza aquí -->
    <h1 v-if="busqueda" class="busqueda-display">{{ busqueda }}</h1>

  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import logo from './assets/logo.ico';
import channelBanner from "./assets/channels4_banner.jpg"

// COMPONENTES
import CanalBanner from './components/CanalBanner.vue'; 
import CanalInfo from './components/CanalInfo.vue'; 
import BusquedaInput from './components/BusquedaInput.vue';
import ChannelNav from './components/ChannelNav.vue'; // Importamos el nuevo componente

// DATA GLOBAL
const Cliente = reactive({
  Nombre: 'Cadif1 Academia Software',
  nroSuscriptores: '4,59 K',
  nroVideos: '170',
  descripcionBreve: 'CADI F1 C.A. Academia de Software. Entrenamos personas en el uso de h... >',
  imgLogo: logo,
  imgBanner: channelBanner 
});

// VARIABLES REACTIVAS
const busqueda = ref(''); 
const suscrito = ref(false); 
</script>

<style>
/* Estilos globales o de la App */
body {
  font-family: 'Roboto', sans-serif; /* Una fuente más estándar para la web */
  margin: 0;
  background-color: #f9f9f9;
}

#perfil-canal {
  max-width: 1280px;
  margin: 0 auto;
  background-color: #fff;
}

.perfil-info-container {
  padding: 0 24px;
}

.nav-and-search-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  border-bottom: 1px solid #ddd;
}

.busqueda-display {
  padding: 20px 24px;
  margin: 0;
  font-size: 24px;
  color: #333;
  min-height: 30px;
  font-weight: 400;
}
</style>
