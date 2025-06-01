<template>
  <div class="flex flex-col items-start">
    <Field :name="fieldName" v-slot="{ field, errorMessage }">
      <label class="block text-gray-300 text-sm font-medium mb-2 text-left" :for="fieldName">{{ label }}</label>
      <slot name="field" v-bind="field" :error="!!errorMessage" />
      <ErrorMessage class="text-red-500 text-xs mt-0.5" :name="fieldName" />
    </Field>
  </div>
</template>
<script setup lang="ts">
import { ErrorMessage, Field } from "vee-validate";

interface Props {
  fieldName: string;
  label?: string;
}

defineProps<Props>();
</script>

