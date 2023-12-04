<template>
  <div class="wrong-letters-container">
    <div class="wrong-letters">
      <p>Errors</p>
      <span v-for="(letter, index) in wrongLetters" :key="letter">
        {{
          index === wrongLetters.length - 1 ? letter : `${letter}, `
        }}
      </span>
    </div>
  </div>
</template>

<script setup lang="ts">
import {defineProps} from "vue";

defineProps<{
  wrongLetters: Array<string>
}>()
</script>
