<template>
  <div id="perfil-canal">

    <div class="banner" :style="{ backgroundImage: 'url(' + Cliente.imgBanner + ')' }">
    </div>

    <div class="perfil-info-container">
      <div class="perfil-info-principal">

        <img :src="Cliente.imgLogo" :alt="'Logo de ' + Cliente.Nombre" class="logo">

        <div class="detalles">
          <h2 class="nombre-canal" :style="{ color: '#212529', fontWeight: '700' }">{{ Cliente.Nombre }}</h2>

          <p class="stats">
            @cadif1academiasoftware ·
            {{ Cliente.nroSuscriptores }} suscriptores ·
            {{ Cliente.nroVideos }} videos
          </p>
        </div>

        <div class="botones-suscripcion">
          <button class="btn-suscribir" :style="{ backgroundColor: 'red', color: 'white', border: 'none' }">
            {{ noSuscrito }}
          </button>

          <button class="btn-suscrito"
            :style="{ backgroundColor: 'rgba(0, 0, 0, 0.1)', color: '#212529', border: '1px solid #ccc' }">
            {{ siSuscrito }}
          </button>
        </div>
      </div>

      <p class="descripcion-breve" :style="{ fontSize: '1em', color: '#6c757d', maxWidth: '80%' }">
        {{ Cliente.descripcionBreve }}
      </p>
    </div>
  </div>

</template>

<script setup>
import { reactive, ref } from 'vue';
import logo from './assets/logo.ico';
import channelBanner from "./assets/channels4_banner.jpg"

// 2. Usando interpolacion "reactive" cree un objeto llamado Cliente
// 3. Agregar datos del canal @Cadif1AcademiaSoftware (datos estimados)

const Cliente = reactive({
  Nombre: 'Cadif1 Academia Software',
  nroSuscriptores: '4,59 K',
  nroVideos: '170',
  descripcionBreve: 'CADI F1 C.A. Academia de Software. Entrenamos personas en el uso de h... >',
  // imagenes
  imgLogo: logo,
  imgBanner: channelBanner 
});


const noSuscrito = ref('Suscribirme');
const siSuscrito = ref('Suscrito');

</script>

<style>
/* Estilos generales */
#perfil-canal {
  font-family: Arial, sans-serif;
  max-width: 1400px;
  margin: 0 auto;
  padding: 20px;
}

/* 5. Banner */
.banner {
  height: 250px;
  background-size: cover;
  background-position: center;
  border-radius: 4px;
  margin-bottom: 25px;
  /* La URL se inyecta vía :style en el template */
}

.perfil-info-container {
  padding: 0 10px;
}

.perfil-info-principal {
  display: flex;
  align-items: center;
  gap: 25px;
  margin-bottom: 20px;
}

/* 5. Logo */
.logo {
  width: 90px;
  height: 90px;
  border-radius: 50%;
  object-fit: cover;
  /* La URL se inyecta vía :src en el template */
}

.detalles {
  flex-grow: 1;
  text-align: left;
}

.detalles h2 {
  margin: 0 0 5px 0;
  font-size: 1.8em;
  /* Los estilos se inyectan vía :style en el template */
}

.stats {
  margin: 0;
  color: #606060;
  font-size: 0.9em;
}

/* 4. Botones de Suscripción */
.botones-suscripcion {
  display: flex;
  gap: 10px;
}

.btn-suscribir,
.btn-suscrito {
  padding: 10px 18px;
  border-radius: 20px;
  font-weight: 500;
  font-size: 0.9em;
  cursor: pointer;
  white-space: nowrap;
  /* Los colores se inyectan vía :style en el template */
  transition: opacity 0.2s;
}

.descripcion-breve {
  text-align: left;
  margin-left: 115px;
  /* Alineado con el nombre del canal */
  /* Los estilos se inyectan vía :style en el template */
}
</style>