<template>
  <div
    v-for="(property, index) in properties"
    :key="index"
    class="card rounded-lg"
  >
    <!-- Parte superior con imagen de ejemplo -->
    <div class="card-img">
      <img :src="property.image" class="rounded-lg" />
    </div>

    <!-- Parte inferior con detalles -->
    <div class="card-details p-4">
      <!-- Título -->
      <h2 class="text-xl font-bold mb-2">{{ property.name }}</h2>

      <!-- Iconos y detalles -->
      <div class="flex items-center mb-2">
        <LucideActivity />
        <i class="icon-lucide-room mr-2"></i>
        <span>{{ property.rooms }} habitaciones</span>
      </div>

      <div class="flex items-center mb-2">
        <LucideMapPin />
        <i class="icon-lucide-location-pin mr-2"></i>
        <span>{{ property.city }}</span>
      </div>

      <div class="flex items-center mb-2">
        <LucideBath />
        <span class="ml-2">{{ property.bathrooms }} baños</span>
      </div>

      <!-- Botón "Ver Propiedad" -->
      <nuxt-link
        :to="'/detalle-propiedad/' + property.id"
        class="bg-blue-500 text-white px-4 py-2 rounded-md w-full"
      >
        Ver Propiedad
      </nuxt-link>
    </div>
  </div>
</template>

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
