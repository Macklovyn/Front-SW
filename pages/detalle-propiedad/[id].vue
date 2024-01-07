<template>
  <div class="grid grid-cols-5 m-30">
    <div></div>
    <div class="mt-5 col-span-3 text-center" style="margin-top: 3rem">
      <h1 class="mt-3 mb-3 font-bold text-3xl" style="margin-bottom: 3rem">
        {{ itemData.name }}
      </h1>
      <img :src="itemData.image" class="rounded-lg mb-5" alt="" />

      <div class="text-justify" style="margin-bottom: 3rem">
        <div class="grid grid-cols-4">
          <div><LucideMapPin /> {{ itemData.city }} Ubicacion</div>
          <div><LucideHome /> {{ itemData.rooms }} Habitaciones</div>
          <div><LucideBath /> {{ itemData.bathrooms }} Baños</div>
          <div>
            <nuxt-link
              :to="'/mensaje-propiedad/' + itemData.id"
              class="bg-blue-500 text-white px-4 py-2 rounded-md w-100"
            >
              Contactar
            </nuxt-link>
          </div>
        </div>

        <br />
        {{ itemData.description }}
      </div>
    </div>
    <div></div>
  </div>
</template>

<script setup>
const route = useRoute();

const itemData = await $fetch(
  `http://localhost:4000/api/properties/${route.params.id}`
);

console.log(itemData);
useHead({
  title: `${itemData.name}`,
});
</script>