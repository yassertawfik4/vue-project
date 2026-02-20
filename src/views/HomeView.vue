<template>
  <div>
    <CarouselBanner />

    <div class="container mx-auto my-5">
      <h2 class="text-center text-[40px] font-bold">Products</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 py-10">
        <ProductCard v-for="p in products" :key="p.id" :product="p" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, toRefs } from "vue";
import CarouselBanner from "@/components/CarouselBanner.vue";
import ProductCard from "@/components/ProductCard.vue";

const { products } = defineProps({
  products: { type: Array, required: true },
});

onMounted(() =>
  console.log(`HomeView mounted — ${products.length} products loaded`),
);
onUnmounted(() => console.log("HomeView unmounted"));
</script>
