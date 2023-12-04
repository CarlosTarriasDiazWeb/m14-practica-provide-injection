<script setup lang="ts">
import { ref } from "vue";
import { inject } from "vue";
import type { InjectionKey, Ref } from "vue";
import { currencyKey } from "@/injection_keys/injection_keys";


//AMB PROPS
// const currencyValue = ref("$");

const props = defineProps<{
    price: number
}>()

const currencyValue = inject<string>(currencyKey);

</script>

<template>
    <span>{{ currencyValue }} {{ price.toFixed(2) }}</span>
</template>

<style scoped></style>
