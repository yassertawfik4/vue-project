<template>
  <div class="container mx-auto my-10">
    <h1 class="text-4xl font-bold mb-4">Yasser Tawfik</h1>
    <h2 class="text-2xl font-semibold mb-2">Course: Vue + DaisyUI — ITI</h2>
    <p>
      Welcome to our small demo store. This project showcases a simple product
      listing, detail pages, and cart-like buy interactions using Vue 3 and
      DaisyUI components.
    </p>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from "vue";

onMounted(() => console.log("AboutView mounted"));
onUnmounted(() => console.log("AboutView unmounted"));
</script>
