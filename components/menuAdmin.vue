<template>
  <div class="grid grid-cols-3 gap-5 mt-5 mx-20 text-center">
    <nuxt-link
      to="/admin/categorias"
      class="font-semibold text-lg border border-black p-5 rounded-xl hover:bg-blue-500 hover:text-white hover:border-blue-700 transition duration-300"
    >
      Categorías
    </nuxt-link>

    <nuxt-link
      to="/admin/propiedades"
      class="font-semibold text-lg border border-black p-5 rounded-xl hover:bg-blue-500 hover:text-white hover:border-blue-700 transition duration-300"
    >
      Propiedades
    </nuxt-link>

    <nuxt-link
      to="/admin/mensajes"
      class="font-semibold text-lg border border-black p-5 rounded-xl hover:bg-blue-500 hover:text-white hover:border-blue-700 transition duration-300"
    >
      Mensajes
    </nuxt-link>
  </div>
</template>
