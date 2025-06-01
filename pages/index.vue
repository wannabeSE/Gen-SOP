<template>
  <div
    class="min-h-screen bg-gradient-to-br from-[#39185a] via-[#07040a] to-[#39185a] relative overflow-hidden"
  >
    <!-- Background decorative elements -->
    <div class="absolute inset-0">
      <div
        class="absolute bottom-0 left-0 w-96 h-96 bg-blue-600/20 rounded-full blur-3xl transform -translate-x-1/2 translate-y-1/2"
      ></div>
      <div
        class="absolute top-1/3 right-0 w-64 h-64 bg-pink-600/20 rounded-full blur-2xl"
      ></div>
    </div>

    <!-- Header -->
    <header class="relative z-10 px-6 py-4">
      <nav class="flex items-center justify-between max-w-7xl mx-auto">
        <!-- Logo -->
        <div class="flex items-center space-x-2">
          <div
            class="w-8 h-8 bg-white rounded-lg flex items-center justify-center"
          >
            <span class="text-black font-bold text-sm">A</span>
          </div>
          <span class="text-white font-semibold text-lg">After</span>
        </div>

        <!-- Navigation -->
        <div class="hidden md:flex items-center space-x-8">
          <a href="#" class="text-gray-300 hover:text-white transition-colors"
            >Home</a
          >
          <a href="#" class="text-gray-300 hover:text-white transition-colors"
            >Plans</a
          >
          <a href="#" class="text-gray-300 hover:text-white transition-colors"
            >Product</a
          >
          <a href="#" class="text-white border-b border-white pb-1">Contact</a>
          <a href="#" class="text-gray-300 hover:text-white transition-colors"
            >About us</a
          >
        </div>

        <!-- Auth buttons -->
        <div class="flex items-center space-x-4">
          <button class="text-gray-300 hover:text-white transition-colors">
            Login
          </button>
          <button
            class="bg-gray-700 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors"
          >
            Get started
          </button>
        </div>
      </nav>
    </header>

    <!-- Main content -->
    <main class="relative z-10 px-6 py-16">
      <div class="max-w-2xl mx-auto text-center">
        <!-- Title -->
        <h1 class="text-5xl md:text-6xl font-bold text-white mb-6">
          Let's Generate a S.O.P 📝
        </h1>

        <!-- Contact Form -->
        <Form
          @submit.prevent="submitForm"
          class="space-y-6"
          :validation-schema="formSchema"
        >
          <!-- First row - Name fields -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <FormField fieldName="firstName" label="First name">
              <template #field="slotProps">
                <FormInput
                  v-bind="slotProps"
                  name="firstName"
                  placeholder="Jonathan"
                />
              </template>
            </FormField>

            <FormField fieldName="lastName" label="Last name">
              <template #field="slotProps">
                <FormInput
                  v-bind="slotProps"
                  name="lastName"
                  placeholder="James"
                />
              </template>
            </FormField>
          </div>

          <!-- Second row - Email and Phone -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <FormField fieldName="email" label="Email">
              <template #field="slotProps">
                <FormInput
                  v-bind="slotProps"
                  name="email"
                  placeholder="Jonathan2718@gmail.com"
                />
              </template>
            </FormField>
            <FormField fieldName="phone" label="Phone number">
              <template #field="slotProps">
                <FormInput
                  v-bind="slotProps"
                  name="phone"
                  placeholder="+91 9876543210"
                  type="number"
                />
              </template>
            </FormField>
          </div>

          <!-- Upload CV/Resume PDF -->
          <FileUpload
            v-model:pdfFile="pdfFile"
            @update:pdfFile="updatePdfFile"
          />
          <!-- Submit button -->
          <button
            type="submit"
            class="w-full bg-gray-700 hover:bg-gray-600 text-white font-medium py-3 px-6 rounded-lg transition-all duration-200 transform hover:scale-[1.02] focus:outline-none focus:ring-2 focus:ring-purple-500"
          >
            Generate S.O.P
          </button>
        </Form>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { FileUpload, FormField, FormInput } from "~/components";
import { Form } from "vee-validate";
import { object, ObjectSchema, string } from "yup";

// Form data
const form = ref({
  firstName: "",
  lastName: "",
  email: "",
  phone: "",
  pdfFile: null,
});
const formSchema: ObjectSchema<object> = object({
  firstName: string().required("First name is required"),
  lastName: string().required("Last name is required"),
  email: string().email("Invalid email").required("Email is required"),
  phone: string()
    .min(11)
    .required("Phone number is required"),
  pdfFile: object().required("PDF file is required"),
});
// UI state
const pdfFile = ref(null);
const updatePdfFile = (file: File) => {
  console.log(file);
};
// Form submission
const submitForm = () => {
  console.log("Form submitted:", form.value);
  // Add your form submission logic here
  // For file handling, you might need to use FormData
  const formData = new FormData();
  formData.append("firstName", form.value.firstName);
  formData.append("lastName", form.value.lastName);
  formData.append("email", form.value.email);
  formData.append("phone", form.value.phone);
};
</script>

<style scoped>
/* Additional custom styles if needed */
</style>
