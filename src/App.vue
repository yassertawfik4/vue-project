<script setup>
import NavBar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
import { RouterView } from "vue-router";
import { ref } from "vue";

const links = [
  { id: 1, name: "Home", path: "/" },
  { id: 2, name: "Products", path: "/product/1" },
  { id: 3, name: "About", path: "/about" },
];

const products = ref([
  {
    id: 1,
    name: "Cozy Sneakers",
    title: "Cozy Sneakers",
    description: "High-quality sneakers that go with everything you wear.",
    image:
      "https://img.daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.webp",
    badge: "NEW",
    price: 120,
    discount: 20,
    stock: 5,
    tags: ["Fashion", "Casual", "Sport"],
  },
  {
    id: 2,
    name: "Classic Loafers",
    title: "Classic Loafers",
    description: "Elegant loafers for formal and casual wear.",
    image:
      "https://img.daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.webp",
    badge: "SALE",
    price: 150,
    discount: 10,
    stock: 2,
    tags: ["Formal", "Leather"],
  },
  {
    id: 3,
    name: "Trail Runners",
    title: "Trail Runners",
    description: "Durable shoes built for outdoor adventures.",
    image:
      "https://img.daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.webp",
    badge: "POPULAR",
    price: 200,
    discount: 25,
    stock: 0,
    tags: ["Sport", "Outdoor"],
  },
]);

function handleBuy(productId) {
  const idx = products.value.findIndex((p) => p.id === Number(productId));
  if (idx !== -1 && products.value[idx].stock > 0) {
    products.value[idx].stock = products.value[idx].stock - 1;
  }
}
</script>

<template class>
  <NavBar :links="links" />
  <RouterView v-slot="{ Component }">
    <component :is="Component" :products="products" @buy="handleBuy" />
  </RouterView>
  <Footer />
</template>
<style scoped></style>
