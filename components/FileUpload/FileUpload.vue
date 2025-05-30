<template>
  <div>
    <label class="block text-gray-300 text-sm font-medium mb-2 text-left">
      Upload CV
    </label>
    <div
      @dragover.prevent="dragover = true"
      @dragleave.prevent="dragover = false"
      @drop.prevent="dropFile"
      class="w-full px-4 py-8 bg-gray-800/50 border-2 border-dashed rounded-lg text-center"
      :class="[
        dragover ? 'border-purple-500 bg-gray-800/70' : 'border-gray-700',
        fileUploaded ? 'border-green-500' : '',
      ]"
    >
      <div v-if="!pdfFile">
        <svg
          class="w-10 h-10 mx-auto text-gray-400 mb-3"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"
          ></path>
        </svg>
        <p class="text-gray-300 mb-1">Drag and drop your CV/Resume here</p>
        <p class="text-gray-500 text-sm mb-3">or</p>
        <label
          class="bg-gray-700 hover:bg-gray-600 text-white font-medium py-2 px-4 rounded-lg cursor-pointer transition-all"
        >
          Browse files
          <input
            @change="selectFile"
            type="file"
            accept=".pdf"
            class="hidden"
          />
        </label>
      </div>
      <div v-else class="text-left">
        <div class="flex items-center">
          <svg
            class="w-8 h-8 text-red-500 mr-2"
            fill="currentColor"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M5 4v3H4a2 2 0 00-2 2v3a2 2 0 002 2h1v2a2 2 0 002 2h6a2 2 0 002-2v-2h1a2 2 0 002-2V9a2 2 0 00-2-2h-1V4a2 2 0 00-2-2H7a2 2 0 00-2 2zm8 0v3H7V4h6zm-6 8v4h6v-4H7z"
              clip-rule="evenodd"
            ></path>
          </svg>
          <span class="text-white">{{ pdfFile.name }}</span>
        </div>
        <div class="mt-2 flex justify-between">
          <span class="text-gray-400 text-sm"
            >{{ (pdfFile.size / 1024 / 1024).toFixed(2) }} MB</span
          >
          <button
            @click.prevent="removeFile"
            class="text-red-400 hover:text-red-500 text-sm"
          >
            Remove
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';

interface Props {
  pdfFile: File | null;
}

const props = defineProps<Props>();
const emit = defineEmits<{
  'update:pdfFile': [file: File | null];
}>();

const dragover = ref(false);
const fileUploaded = ref(false);

// Update fileUploaded when pdfFile changes
watch(() => props.pdfFile, (newFile) => {
  fileUploaded.value = !!newFile;
}, { immediate: true });

// File handling methods
const selectFile = (event: Event) => {
  const target = event.target as HTMLInputElement;
  const file = target.files?.[0];
  if (file && file.type === "application/pdf") {
    emit('update:pdfFile', file);
  }
};

const dropFile = (event: DragEvent) => {
  dragover.value = false;
  const file = event.dataTransfer?.files[0];
  if (file && file.type === "application/pdf") {
    emit('update:pdfFile', file);
  }
};

const removeFile = () => {
  emit('update:pdfFile', null);
};
</script>
