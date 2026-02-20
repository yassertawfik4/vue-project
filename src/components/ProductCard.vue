<script setup>
import { onMounted, onUnmounted } from "vue";

const { product } = defineProps({
  product: {
    type: Object,
    required: true,
  },
});

const getDiscountedPrice = (price, discount) => {
  return ((price * (100 - discount)) / 100).toFixed(2);
};

onMounted(() => console.log(`ProductCard mounted — id: ${product.id}`));
onUnmounted(() => console.log(`ProductCard unmounted — id: ${product.id}`));
</script>
<template>
  <div class="container mx-auto my-5">
    <h2 class="text-center text-[40px] font-bold">Related Products</h2>

    <div class="flex flex-wrap gap-4 justify-center py-10">
      <div class="card bg-base-100 w-96 shadow-sm">
        <figure>
          <img :src="product.image" :alt="product.title" />
        </figure>
        <div class="card-body">
          <h2 class="card-title">{{ product.title }}</h2>
          <p>{{ product.description }}</p>

          <div
            class="flex items-center gap-2 my-3"
            v-if="product.price !== undefined && product.discount !== undefined"
          >
            <span class="text-2xl font-bold text-primary"
              >${{ getDiscountedPrice(product.price, product.discount) }}</span
            >
            <span
              v-if="product.discount > 0"
              class="text-sm line-through text-gray-500"
              >${{ product.price }}</span
            >
            <div
              v-if="product.discount > 0"
              class="badge badge-error text-white text-xs"
            >
              -{{ product.discount }}%
            </div>
          </div>

          <div class="card-actions justify-end">
            <router-link
              :to="{ name: 'Product', params: { id: product.id } }"
              class="btn btn-primary"
            >
              View Product
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
