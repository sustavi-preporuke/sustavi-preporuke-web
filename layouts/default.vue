<script setup lang="ts">
import { initFlowbite } from 'flowbite'

onMounted(() => {
    initFlowbite();
})
</script>

<template>
  <div class="bg-white dark:bg-gray-900">
    <Navbar />
    <slot></slot>
  </div>

</template>

<style scoped></style>