<template>
  <div class="notification-container" :class="{show: isVisible}">
    <p>Вы уже вводили этот символ</p>
  </div>
</template>

<script setup lang="ts">
import {defineExpose, ref} from "vue";

  const isVisible = ref(false)
  const openModal = () =>{
    isVisible.value = true
  }
  const closeModal = () =>{
    isVisible.value = false
  }

  defineExpose({
    openModal, closeModal
  })
</script>
