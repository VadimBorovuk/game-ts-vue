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
    setTimeout(()=> notification.value?.closeModal(), 2000)
    return
  }

  if (/^[a-zA-Z]$/.test(key)) {
    letters.value.push(key.toLowerCase())
  }
})
const notification = ref<InstanceType<typeof GameNotification> | null>(null)
const word = ref<string>('basketball')
const letters = ref<string[]>([])

const currectLetters = computed(() => letters.value.filter(x => word.value.includes(x)))
const wrongLetters = computed(() => letters.value.filter(x => !word.value.includes(x)))

// watch(wrongLetters, (value) => {
//   if(value.length >= 6){
//     letters.value = []
//   }
//   console.log(`value`, value)
// })

</script>

<template>
  <main>
    {{ letters }}
    <game-header title="Game" description="write correct word"/>
    <div class="game-container">
      <game-figure :wrongLettersCount="wrongLetters.length"/>
      <game-errors :wrongLetters="wrongLetters"/>
      <game-word :word="word" :currectLetters="currectLetters"/>
    </div>
    <game-popup :word="word"/>
    <game-notification ref="notification"/>
  </main>
</template>



