<script setup>
import { defineProps } from "vue";

const props = defineProps({
  name: String,
  user: String,
  email: String,
  phone: String,
});
</script>
<template>
  <div class="card p-2">
    <h3>This user is called {{ props.name }}</h3>
    <p>Their username is {{ props.user }}</p>
    <p>
      Their contact email is {{ props.email }}, and they can be reached at phone
      number: {{ props.phone }}
    </p>
  </div>
</template>
<style scoped></style>
