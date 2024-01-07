<template>
  <nav class="bg-gray-800 py-4 relative">
    <div class="container mx-auto flex flex-grow justify-between">
      <div>
        <span class="text-white"></span>

        <router-link to="/">
          <LucideHome color="white" class="ml-5" />
        </router-link>
      </div>

      <div class="md:block top-20 md:top-0" :class="{ hidden: menu }">
        <nuxt-link to="/admin/" href="">
          <LucideUser color="white" class="mr-5" />
        </nuxt-link>
      </div>
      <div class="md:hidden text-white">
        <LucideAlignJustify color="white" class="mr-5" @click="openMenu()" />
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";

const menu = ref(false);

const openMenu = () => {
  if (!menu.value) {
    menu.value = true;
  } else {
    menu.value = false;
  }

  console.log(menu.value);
};
</script>