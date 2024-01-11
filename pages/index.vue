<template>
  <div class="mx-auto max-w-screen-xl p-4">
    <div class="mt-4 grid grid-cols-5 gap-4">
      <div class="mx-4">
        <div
          v-for="(categoria, index) in categorias"
          :key="index"
          class="border-2 border-gray-300 mb-1 p-2 text-center font-bold rounded-xl bg-slate-400"
        >
          {{ categoria.name }}
        </div>
      </div>
      <div class="grid grid-cols-4 gap-4 mx-4 col-span-4">
        <PropertyCard :properties="propiedades" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";
import PropertyCard from "@/components/PropertyCard.vue";

const categorias = ref([]);
const propiedades = ref([]);
const getCategories = () => {
  axios.get("https://api-proyectsw.onrender.com/api/categories").then((result) => {
    categorias.value = result.data;
  });

  axios.get("https://api-proyectsw.onrender.com/api/properties").then((result) => {
    propiedades.value = result.data;
  });
};

getCategories();
</script>

<style scoped>
/* Estilos específicos del componente de tarjeta */
.card {
  border: 1px solid #ccc;
  overflow: hidden;
}

.card-img img {
  width: 100%;
  height: 200px; /* Ajusta la altura según tus necesidades */
  object-fit: cover;
}

.card-details {
  background-color: #f9f9f9;
}

.card-details i {
  font-size: 18px;
  margin-right: 5px;
}
</style>