<template>
  <div class="popup-container" v-show="isVisible">
    <div class="popup">
      <h2 v-if="gameStatus === 'win'">You win 😃</h2>
      <template v-else>
        <h2>You lose 😕</h2>
        <h3>...word: {{ word }}</h3>
      </template>
      <button @click="emit('restart')">Сыграть еще раз</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import {defineEmits,
  defineExpose,
  defineProps,
  ref}
  from "vue";
import type {GameStatus} from "@/types/GameStatus";

const gameStatus = ref<GameStatus | null>(null)

const isVisible = ref(false)

const openModal = (status: GameStatus) => {
  gameStatus.value = status
  isVisible.value = true
}
const closeModal = () => {
  isVisible.value = false
}

defineExpose({
  openModal, closeModal
})

const emit = defineEmits<{
  (e: 'restart'): void
}>()

defineProps<{
  word: string
}>()
</script>
