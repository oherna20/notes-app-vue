<template>
    <div
      class="absolute inset-0 w-screen h-screen bg-green-800 flex justify-center items-center"
    >
    <button @click="reset" class="text-white absolute top-2 left-2">
        <whh:exitalt class="text-6xl" />
      </button>
      <form @submit.prevent class="space-y-4">
        <div class="flex flex-col">
          <label for="title" class="text-white mb-2">Title</label>
          <input
            type="text"
            name="title"
            class="rounded py-2 px-4"
            placeholder="Title"
            v-model="newNote.title"
          />
        </div>
        <div class="flex flex-col">
          <label for="content" class="text-white mb-2">Content</label>
          <textarea
            name="content"
            class="rounded py-2 px-4"
            placeholder="Note Content"
            v-model="newNote.content"
          />
        </div>
        <div>
          <button
          v-if="noteToEdit"
          @click="saveNote"
          class="w-full bg-green-500 text-green-800 p-2 rounded mt-4 hover:bg-green-600 hover:text-green-900"
        >
          Save
        </button>
        <button
          v-else
          @click="addNote"
            class="w-full bg-white text-yellow-800 p-2 rounded mt-4 hover:bg-warmGray-300 hover:text-yellow-900"
          >
            Add
          </button>
        </div>
      </form>
    </div>
  </template>
  
  <script setup>
import { reactive, defineEmit, onMounted } from 'vue'
import { showToggle, add, noteToEdit, save } from '~/helpers/useNotes'
const newNote = reactive({
  title: '',
  content: '',
})
onMounted(() => {
  if (noteToEdit.value) {
    newNote.title = noteToEdit.value.title
    newNote.content = noteToEdit.value.content
  }
})
const emit = defineEmit(['added', 'saved'])
const reset = event => {
  showToggle()
  newNote.title = ''
  newNote.content = ''
  noteToEdit.value = null
  emit(event)
}
const addNote = async () => {
  await add(newNote)
  reset('added')
}
const saveNote = async () => {
  await save({ id: noteToEdit.value.id, ...newNote })
  reset('saved')
}  </script>