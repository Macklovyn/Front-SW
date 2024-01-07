<template>
  <div class="grid grid-cols-3 gap-5 mt-5 mx-20 text-center">
    <nuxt-link
      to="/admin/categorias"
      class="font-bold text-2xl border-2 p-5 rounded-xl border-slate-900 bg-slate-300 text-center"
    >
      Categorias
    </nuxt-link>

    <nuxt-link
      to="/admin/propiedades"
      class="font-bold text-2xl border-2 p-5 rounded-xl border-slate-900 bg-slate-300 text-center"
    >
      Propiedades
    </nuxt-link>

    <nuxt-link
      to="/admin/mensajes"
      class="font-bold text-2xl border-2 p-5 rounded-xl border-slate-900 bg-slate-300 text-center"
    >
      Mensajes
    </nuxt-link>
  </div>
</template>