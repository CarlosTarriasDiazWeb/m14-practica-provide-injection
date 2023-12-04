<script setup lang="ts">
import { reactive, ref, watch, type Ref } from 'vue';
import type { Order } from "@/interfaces/Order";
import Comanda from './components/Comanda.vue';
import { provide } from 'vue';
import type { InjectionKey } from "vue";
import { currencyKey } from "@/injection_keys/injection_keys";

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

function currencyConversion(oldCurrency: string, newCurrency: string) {
  if (oldCurrency === "$" && newCurrency === "€") {
    orders.value = orders.value.map(order => ({ ...order, price: order.price * 0.92 }));
  } else if (oldCurrency === "€" && newCurrency === "$") {
    orders.value = orders.value.map(order => ({ ...order, price: order.price * 1.09 }));
  }
}
const orderName: Ref<string> = ref("");

const currency: Ref<string> = ref("$");

watch(currency, (newValue, oldValue) => {
  currencyConversion(oldValue, newValue);
});

provide(currencyKey, currency);

let orders = ref<Order[]>(
  [
    { name: "Hamburger 🍔.", price: 5.01 },
    { name: "Cheeseburger 🧀", price: 6.00 },
    { name: "Impossible Burger 🥕", price: 7.00 },
    { name: "Fries 🍟", price: 2.00 }
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
    <section>
      <label for="currencySelect">Currency
        <select id="currencySelect" v-model="currency">
          <optgroup>
            <option value="$">$</option>
            <option value="€">€</option>
          </optgroup>
        </select>
      </label>
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
