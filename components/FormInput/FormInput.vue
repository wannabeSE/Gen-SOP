<template>
  <input
    :id="id"
    :name="name"
    :type="inputType"
    :placeholder="placeholder"
    class="w-full px-4 py-3 bg-gray-800/80 border border-gray-700 rounded-lg text-white placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent transition-all"
  />
</template>
<script setup lang="ts">
import { defineProps } from "vue";
interface Props {
  id?: string;
  name: string;
  inputType?: string;
  placeholder?: string;
  required?: boolean;
  className?: string;
  error?: boolean;
}
withDefaults(defineProps<Props>(), {
  inputType: "text",
  placeholder: "",
});
</script>

<style scoped>
/* handling autofill color change*/
input:-webkit-autofill {
  -webkit-box-shadow: 0 0 0 30px rgba(31, 41, 55, 0.5) inset;
  box-shadow: 30px 30px 30px 30px #1e2939 inset;
  -webkit-text-fill-color: white;
}

input:-webkit-autofill:focus {
  -webkit-box-shadow: 0 0 0 30px inset;
  box-shadow: 0 0 0 30px #1e2939 inset;
}
</style>
