<template>
  <q-card outline bordered :class="`my-card ${text}`" :style="`${styles}`">
    <q-card-section>
      <div class="text-h6">{{ title }}</div>
    </q-card-section>

    <q-card-section class="q-pt-none text-h2"> {{ value }} </q-card-section>
  </q-card>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  value: {
    type: Number,
    required: true,
  },
  text: {
    type: String,
    required: false,
  },
  styles: {
    type: String,
    required: false,
  },
});
</script>
