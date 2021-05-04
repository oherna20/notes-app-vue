<template>
    <div
      class="bg-white text-yellow-800 rounded space-y-2 flex justify-center items-center"
    >
      <button
      @click="showToggle"
        class="opacity-40 transform transition-all hover:scale-110 hover:opacity-60"
      >
        <pixelarticons:notes-plus class="w-40 h-40 40" />
      </button>
    </div>
  </template>
  
<script setup>
import { showToggle } from '~/helpers/useNotes'
</script>