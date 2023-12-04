<script setup lang="ts">
import type { Order } from "@/interfaces/Order";
import Currency from "./Currency.vue";

const props = defineProps<{
    name: string,
    price: number
}>()

const emit = defineEmits<{
    addOrder: [order: Order]
}>()

function sendOrder() {
    const orderToSend: Order = { name: props.name, price: props.price }
    emit('addOrder', orderToSend);
}

</script>

<template>
    <article class="d-flex gap-1">
        <p>{{ name }}</p>
        <span>{{ price.toFixed(2) }}</span>
        <Currency></Currency>
        <input type="button" @click="sendOrder" value="Add to Cart">
    </article>
</template>

<style scoped></style>
