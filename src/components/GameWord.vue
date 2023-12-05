<template>
  <div class="word">
    <span v-for="(letter, idx) in word" :key="idx" class="letter">
      {{ correctLetters.includes(letter) ? letter : '' }}
    </span>
  </div>
</template>

<script setup lang="ts">
import {defineProps} from "vue";

defineProps<{
  word: string
  correctLetters: Array<string>
}>()
</script>
