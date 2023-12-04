<template>
  <h1>{{title}}</h1>
  <p>{{description}}</p>
</template>

<script setup lang="ts">
  import {defineProps} from "vue";

  defineProps<{
    title: string
    description: string
  }>()
</script>
