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
          @submit="submitForm"
          class="space-y-6"
          :validation-schema="formSchema"
        >
          <!-- First row - Name fields -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <!-- Dynamic form fields -->
            <div v-for="field in formFields" :key="field.fieldName">
              <FormField :fieldName="field.fieldName" :label="field.label">
                <template #field="slotProps">
                  <div class="w-full">
                    <FormInput
                      v-bind="slotProps"
                      :name="field.fieldName"
                      :placeholder="field.placeholder"
                      :type="field.type"
                    />
                  </div>
                </template>
              </FormField>
            </div>
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

interface FormField {
  fieldName: string;
  label: string;
  type: string;
  placeholder: string;
}
const formSchema: ObjectSchema<object> = object({
  firstName: string().required("First name is required"),
  lastName: string().required("Last name is required"),
  email: string().email("Invalid email").required("Email is required"),
  phone: string().min(11).required("Phone number is required"),
  ownUniversityName: string().min(10).required("University Name is required"),
  degree: string().min(10).required("Degree is required"),
  preferredUniversity: string().min(10).required("University Name is required"),
});

// dynamic form fields
const formFields: FormField[] = [
  {
    fieldName: "firstName",
    label: "First name",
    type: "text",
    placeholder: "Jonathan",
  },
  {
    fieldName: "lastName",
    label: "Last name",
    type: "text",
    placeholder: "James",
  },
  {
    fieldName: "email",
    label: "Email",
    type: "email",
    placeholder: "Jonathan2718@gmail.com",
  },
  {
    fieldName: "phone",
    label: "Phone number",
    type: "number",
    placeholder: "+91 9876543210",
  },
  {
    fieldName: "ownUniversityName",
    label: "Your University Name",
    type: "text",
    placeholder: "University of Dhaka",
  },
  {
    fieldName: "degree",
    label: "Degree",
    type: "text",
    placeholder: "Bachelor of Science",
  },
  {
    fieldName: "preferredUniversity",
    label: "Preferred University",
    type: "text",
    placeholder: "University of Dhaka",
  },
];
// UI state
const pdfFile = ref(null);
const updatePdfFile = (file: File) => {
  console.log(file);
};
// Form submission
const submitForm = (values: any) => {
  console.log("Form submitted:", values);
};
</script>

<style scoped>
/* Additional custom styles if needed */
</style>
