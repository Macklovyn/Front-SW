<template>
  <div
    v-for="(property, index) in properties"
    :key="index"
    class="card rounded-lg shadow-md border border-gray-200 overflow-hidden"
  >
    <!-- Parte superior con imagen de ejemplo -->
    <div class="card-img">
      <img :src="property.image" class="rounded-t-lg" />
    </div>

    <!-- Parte inferior con detalles -->
    <div class="card-details p-4">
      <!-- Título -->
      <h2 class="text-xl font-bold mb-2">{{ property.name }}</h2>

      <!-- Iconos y detalles -->
      <div class="flex items-center mb-2">
        <i class="icon-lucide-room text-gray-500 mr-2"></i>
        <span class="text-gray-700">{{ property.rooms }} habitaciones</span>
      </div>

      <div class="flex items-center mb-2">
        <i class="icon-lucide-location-pin text-gray-500 mr-2"></i>
        <span class="text-gray-700">{{ property.city }}</span>
      </div>

      <div class="flex items-center mb-2">
        <i class="icon-lucide-bath text-gray-500 mr-2"></i>
        <span class="text-gray-700">{{ property.bathrooms }} baños</span>
      </div>

      <!-- Botón "Ver Propiedad" -->
      <nuxt-link
        :to="'/detalle-propiedad/' + property.id"
        class="bg-blue-500 text-white px-4 py-2 rounded-md w-full inline-block text-center"
      >
        Ver Propiedad
      </nuxt-link>
    </div>
  </div>
</template>

<style scoped>
.card {
  transition: transform 0.2s ease-in-out;
}

.card:hover {
  transform: scale(1.02);
}
</style>

<script>
export default {
  props: {
    properties: {
      type: Array,
      required: true,
    },
  },
};
</script>
