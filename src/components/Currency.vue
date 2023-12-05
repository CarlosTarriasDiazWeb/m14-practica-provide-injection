<script setup lang="ts">
import { inject, type Ref } from "vue";
import { currencyKey } from "@/injection_keys/injection_keys";

//El dòlar és el valor per defecte
const currencyValue = inject<string>(currencyKey, '$');

</script>

<template>
    <span>{{ currencyValue }}</span>
</template>

<style scoped></style>
