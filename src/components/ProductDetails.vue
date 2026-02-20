<script setup>
import { computed, onMounted, onUnmounted } from "vue";

const { product } = defineProps({
  product: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["buy"]);

const heroDiscountedPrice = computed(() => {
  const p = product;
  return p && p.price !== undefined && p.discount !== undefined
    ? ((p.price * (100 - p.discount)) / 100).toFixed(2)
    : "0.00";
});

onMounted(() => console.log(`ProductDetails mounted — id: ${product.id}`));
onUnmounted(() => console.log(`ProductDetails unmounted — id: ${product.id}`));
</script>
<template>
  <div class="hero bg-base-200 min-h-screen">
    <div class="hero-content flex-col lg:flex-row gap-8">
      <figure class="relative">
        <img
          :src="product.image"
          :alt="product.name"
          :class="'max-w-2xl rounded-lg shadow-2xl w-full h-full'"
        />
        <div
          v-if="product.badge"
          class="badge badge-primary absolute top-4 right-4 text-lg"
        >
          {{ product.badge }}
        </div>
      </figure>
      <div>
        <h1 class="text-5xl font-bold">{{ product.name }}</h1>
        <p class="py-6 text-lg">{{ product.description }}</p>

        <div class="flex gap-2 flex-wrap my-4">
          <div
            v-for="tag in product.tags"
            :key="tag"
            class="badge badge-outline"
          >
            {{ tag }}
          </div>
        </div>

        <div class="flex items-center gap-4 my-6">
          <div class="flex items-center gap-2">
            <span class="text-4xl font-bold text-primary"
              >${{ heroDiscountedPrice }}</span
            >
            <span
              v-if="product.discount > 0"
              class="text-xl line-through text-gray-500"
              >${{ product.price }}</span
            >
          </div>
          <div
            v-if="product.discount > 0"
            class="badge badge-error text-white text-sm"
          >
            -{{ product.discount }}%
          </div>
        </div>

        <div class="mb-4">
          <span class="font-medium">Stock:</span>
          <span v-if="product.stock > 0"> {{ product.stock }}</span>
          <span v-else class="text-red-600 font-bold"> Out of Stock</span>
        </div>

        <button
          class="btn btn-primary btn-lg"
          :disabled="product.stock === 0"
          @click="emit('buy', product.id)"
        >
          Buy Now
        </button>
      </div>
    </div>
  </div>
</template>
