<template>
  <div>
    <headerUser/>
    <slot />
  </div>
</template>

<script setup>
import headerUser from '@/components/headerUser.vue'
</script>