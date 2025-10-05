<template>
  <div class="info-container">
    <img :src="Cliente.imgLogo" alt="Logo del canal" class="channel-logo">
    
    <!-- Contenido condicional -->
    <div class="channel-text" :class="{ 'suscrito-true': suscrito, 'suscrito-false': !suscrito }">
      <h2>{{ Cliente.Nombre }}</h2>
      <span>{{ Cliente.nroSuscriptores }} suscriptores</span>
      <span>&nbsp;•&nbsp;</span>
      <span>{{ Cliente.nroVideos }} videos</span>
      <p>{{ Cliente.descripcionBreve }}</p>
    </div>

    <!-- Botón estado de suscripción -->
    <button @click="toggleSuscripcion" :class="{ 'suscrito-btn': suscrito }">
      {{ suscrito ? 'Suscrito' : 'Suscribirse' }}
    </button>
  </div>
</template>

<script setup>
const props = defineProps({
  Cliente: {
    type: Object,
    required: true
  },
  suscrito: {
    type: Boolean,
    required: true
  }
});

// Emitirá un evento para que el componente padre (App.vue) actualice el estado
const emit = defineEmits(['update:suscrito']);

const toggleSuscripcion = () => {
  // Emitimos el evento con el valor contrario al actual
  emit('update:suscrito', !props.suscrito);
};
</script>

<style scoped>
.info-container {
  display: flex;
  align-items: center;
  padding: 15px;
  gap: 20px;
}

.channel-logo {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
}

/* Estilos condicionales */
.suscrito-true {
  text-transform: uppercase; /* Muestra en mayúsculas si está suscrito */
}

.suscrito-false {
  font-style: italic; /* Muestra en cursiva si no está suscrito */
}

.channel-text h2 {
  margin: 0;
}

.channel-text span, .channel-text p {
  font-size: 14px;
  color: #606060;
}

.channel-text p {
  margin-top: 5px;
}

button {
  background-color: #cc0000;
  color: white;
  border: none;
  border-radius: 20px;
  padding: 10px 20px;
  font-weight: bold;
  cursor: pointer;
  margin-left: auto; /* Empuja el botón a la derecha */
}

button.suscrito-btn {
  background-color: #606060;
}
</style>
