<template>
  <p>UserData component:</p>
  <h2>{{ name }}</h2>
  <h3>{{ age }}</h3>
  <p>{{ fullName }}</p>
</template>

<script setup>
import { computed, defineProps } from 'vue';

const props = defineProps({
  name: {
    type: String
  },
  age: {
    type: Number
  },
  lastName: {
    type: String
  },
})

const fullName = computed(() => props.name + ' ' + props.lastName)
</script>
