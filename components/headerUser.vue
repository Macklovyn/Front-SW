<template>
  <nav class="bg-black py-4 relative">
    <div class="container mx-auto flex flex-grow justify-between items-center">
      <div class="flex items-center">
        <span class="text-white text-lg font-semibold"></span>

        <router-link to="/">
          <LucideHome color="white" class="ml-5 h-8 w-8" />
        </router-link>
      </div>

      <div class="md:block top-20 md:top-0" :class="{ hidden: menu }">
        <nuxt-link to="/admin/" href="">
          <LucideUser color="white" class="mr-5 h-8 w-8" />
        </nuxt-link>
      </div>

      <div class="md:hidden text-white">
        <LucideAlignJustify color="white" class="mr-5 h-8 w-8" @click="openMenu" />
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";

const menu = ref(false);

const openMenu = () => {
  menu.value = !menu.value;
  console.log(menu.value);
};
</script>
