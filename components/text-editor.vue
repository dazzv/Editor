<script setup lang="ts">
import { defineEmits } from 'vue';

const updateHTML = (e: MouseEvent) => {
  emit('input', (e.target as HTMLElement).innerHTML);
};

const emit = defineEmits();
</script>

<template>
  <div @input="event => updateHTML" class="cursor-text border-none text-gray-200 outline-none" 
    contenteditable="true" data-placeholder="Your history...">
  </div>
</template>

<style scoped>
.text-editor:empty:before {
  content:attr(data-placeholder);
  color:#6b7280;
}
</style>