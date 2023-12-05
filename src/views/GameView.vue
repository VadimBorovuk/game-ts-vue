<template>
  <main>
    <game-header title="Game" description="write correct word"/>
    <div class="game-container">
      <game-figure :wrongLettersCount="wrongLetters.length"/>
      <game-errors :wrongLetters="wrongLetters"/>
      <game-word :word="word" :correctLetters="correctLetters"/>
    </div>
    <game-popup ref="popup" :word="word" @restart="restart"/>
    <game-notification ref="notification"/>
  </main>
</template>

<script setup lang="ts">
import GameHeader from '../components/GameHeader.vue'
import GameFigure from '../components/GameFigure.vue'
import GameErrors from '../components/GameErrors.vue'
import GameWord from '../components/GameWord.vue'
import GameNotification from '../components/GameNotification.vue'
import GamePopup from '../components/GamePopup.vue'

import {computed, ref, watch} from 'vue'

window.addEventListener('keydown', ({key}) => {
  if (letters.value.includes(key)) {
    notification.value?.openModal()
    setTimeout(() => notification.value?.closeModal(), 2000)
    return
  }

  if (/^[a-zA-Z]$/.test(key)) {
    letters.value.push(key.toLowerCase())
  }
})
const notification = ref<InstanceType<typeof GameNotification> | null>(null)
const popup = ref<InstanceType<typeof GamePopup> | null>(null)
const word = ref<string>('cheese')
const letters = ref<string[]>([])

const correctLetters = computed(() => letters.value.filter(x => word.value.includes(x)))
const wrongLetters = computed(() => letters.value.filter(x => !word.value.includes(x)))

const restart = () => {
  letters.value = []
  popup.value?.closeModal()
}

watch(wrongLetters, (value) => {
  if(value.length === 6){
    popup.value?.openModal('lose')
  }
})

watch(correctLetters, (value) => {
  if([...word.value].every(x => correctLetters.value.includes(x))){
    popup.value?.openModal('win')
  }
})

</script>




