<script setup lang="ts">
import { reactive, ref, type Ref } from 'vue';
import type { Order } from "@/interfaces/Order";
import Comanda from './components/Comanda.vue';


function showOrderAlert() {

  if (orderName.value.length > 0) {
    alert("Your order has been placed!")
  };
}

function showStoreAlert(order: Order) {
  console.log(order)
  storage.value.push(order);

  const ordersNames = storage.value.map(order => order.name).join(", ");
  alert(ordersNames);
}

const orderName: Ref<string> = ref("");

const orders = reactive<Order[]>(
  [
    { name: "Hamburger 🍔.", price: 5 },
    { name: "Cheeseburger 🧀", price: 6 },
    { name: "Impossible Burger 🥕", price: 7 },
    { name: "Fries 🍟", price: 2 }
  ]
);

const storage: Ref<Order[]> = ref([]);

</script>

<template>
  <main class="d-flex flex-column justify-content-center align-items-center gap-3">
    <h1>{{ orderName }}</h1>
    <section>
      <input type="text" v-model.trim="orderName">
      <input type="button" @click="showOrderAlert" value="Place Order">
    </section>
    <section class="d-flex flex-column gap-2">
      <Comanda @addOrder="showStoreAlert" v-for="order in orders" :key="order.name" :name="order.name"
        :price="order.price"></Comanda>
    </section>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
}
</style>
