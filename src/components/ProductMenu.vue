<script setup>
import { defineProps, defineEmits } from 'vue';

defineProps(['data']);

const emit = defineEmits(['add-cart']);

</script>

<template>
  <div class="list-group">
    <a href="#" class="list-group-item list-group-item-action" v-for="drink in data" :key="drink.id" @click.prevent="emit('add-cart', drink)">
      <div class="d-flex w-100 justify-content-between">
        <h5 class="mb-1">{{ drink.name }}</h5>
        <small>${{ drink.price }}</small>
      </div>
      <p class="mb-1">{{ drink.description }}</p>
    </a>
  </div>
</template>
