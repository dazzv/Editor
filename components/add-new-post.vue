<script setup lang="ts">

interface post {
  title: string,
  username: string,
  text?: string,
  date?: string
}
const content = ref<post>({
  title: "",
  username: "",
  text: "",
  date: "",
});

const showEditorElements = ref<boolean>(true)

const saveEditText = (action:string): void => {
  content.value.text = document.querySelector('.text-editor')?.innerHTML // get editor content
  content.value.date = new Date().toLocaleString().slice(0, 17) // get locale time

  const editorText = document.querySelector('.text-editor') // editor text
  const outerText = document.querySelector('.outerText') // space for output text

  // transfer the contents
  if(action === 'save' && editorText && outerText) {
    outerText.innerHTML = editorText.innerHTML

    showEditorElements.value = false
  } 
  else if (action === 'edit' && outerText && editorText) {
    editorText.innerHTML = outerText.innerHTML
    
    showEditorElements.value = true
  }
}
</script>

<template>
  <section class="transition-transform ease-in-out max-sm:px-2">
    
    <div v-show="showEditorElements" class="mx-auto max-w-md md:max-w-2xl flex flex-col pt-8 h-full">
      <div class="flex items-center justify-between">
        <input class="pb-4 outline-none text-gray-200 bg-gray-800 placeholder-gray-400 text-3xl w-full" v-model="content.title" type="text" placeholder="Title" maxlength="70"/>
        <button @click="saveEditText('save')" class="px-4 py-1 text-gray-300 bg-gray-700 rounded ml-4 min-w-20 max-w-24">Publish</button>
      </div>
      <input class="pb-4 outline-none text-gray-500 text-small bg-gray-800 placeholder-gray-600" v-model="content.username" placeholder="Author" maxlength="20"/>
      <text-editor-actions class="flex justify-end" />
      <text-editor class="text-editor w-full min-h-screen" />
    </div>

    <div v-show="!showEditorElements" class="mx-auto max-w-md md:max-w-2xl flex flex-col pt-8">
      <div class="flex items-center justify-between">
        <h1 class="pb-4 text-gray-200 text-3xl w-full">{{ content.title }}</h1>
        <button @click="saveEditText('edit')" class="px-4 py-1 text-gray-300 bg-gray-700 rounded ml-4 min-w-20 max-w-24">Edit</button>
      </div>
      <p class="pb-4 text-gray-500 text-small bg-gray-800">{{ content.username }}</p>
      <p class="outerText text-gray-200 w-full mt-[35px]"></p>
      <span class="self-end text-small text-gray-500">{{ content.date }}</span>
    </div>

  </section>
</template>