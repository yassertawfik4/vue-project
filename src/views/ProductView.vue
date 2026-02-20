<template>
  <div>
    <ProductDetails v-if="product" :product="product" @buy="onBuy" />

    <div class="container mx-auto my-8">
      <h3 class="text-2xl font-bold mb-4">Related Products</h3>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <ProductCard v-for="item in relatedProducts" :key="item.id" :product="item" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, computed } from "vue";
import { useRoute } from "vue-router";
import ProductDetails from "@/components/ProductDetails.vue";
import ProductCard from "@/components/ProductCard.vue";

const props = defineProps({
  products: { type: Array, required: true },
});

const route = useRoute();
const emit = defineEmits(["buy"]);

const productId = computed(() => Number(route.params.id));
const product = computed(() => props.products.find((p) => p.id === productId.value) || null);
const relatedProducts = computed(() => props.products.filter((p) => p.id !== productId.value));

onMounted(() => {
  console.log(`ProductView mounted for ID: ${route.params.id}`);
});

onUnmounted(() => console.log("ProductView unmounted"));

function onBuy(productId) {
  emit("buy", productId);
}
</script>
