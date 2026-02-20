<script setup>
import { onMounted, onUnmounted } from "vue";

const { links } = defineProps({
  links: {
    type: Array,
    default: () => [],
  },
});

onMounted(() => console.log("NavBar mounted"));
onUnmounted(() => console.log("NavBar unmounted"));
</script>

<template>
  <div class="container mx-auto">
    <div class="navbar bg-base-100">
      <div class="flex-1">
        <RouterLink to="/" class="btn btn-ghost text-xl">daisyUI</RouterLink>
      </div>
      <div class="flex-none">
        <ul class="menu menu-horizontal px-1">
          <li v-for="link in links" :key="link.id">
            <RouterLink :to="link.path">{{ link.name }}</RouterLink>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
