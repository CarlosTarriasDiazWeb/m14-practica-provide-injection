<script setup lang="ts">
import { ref } from "vue";
import { inject } from "vue";
import type { InjectionKey, Ref } from "vue";
import { currencyKey } from "@/injection_keys/injection_keys";


//AMB PROPS
// const currencyValue = ref("$");

const currencyValue = inject<string>(currencyKey);

</script>

<template>
    <span>{{ currencyValue }}</span>
</template>

<style scoped></style>
