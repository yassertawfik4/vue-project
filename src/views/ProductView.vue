<template>
  <div>
    <ProductDetails v-if="product" :product="product" @buy="onBuy" />

    <div class="container mx-auto my-8">
      <h3 class="text-2xl font-bold mb-4">Related Products</h3>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <ProductCard v-for="p in related" :key="p.id" :product="p" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref, watch } from "vue";
import { useRoute } from "vue-router";
import ProductDetails from "@/components/ProductDetails.vue";
import ProductCard from "@/components/ProductCard.vue";

const props = defineProps({
  products: { type: Array, required: true },
});

const route = useRoute();
const product = ref(null);
const related = ref([]);
const emit = defineEmits(["buy"]);

function findProduct() {
  const id = Number(route.params.id);
  product.value = props.products.find((p) => p.id === id) || null;
  related.value = props.products.filter((p) => p.id !== id);
}

onMounted(() => {
  findProduct();
  console.log(`ProductView mounted for ID: ${route.params.id}`);
});

onUnmounted(() => console.log("ProductView unmounted"));

watch(
  () => route.params.id,
  () => {
    findProduct();
  },
);

function onBuy(productId) {
  emit("buy", productId);
}
</script>
