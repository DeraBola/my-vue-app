<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg?: string }>()

const name = ref('')
const email = ref('')
const alert = ref<{ type: 'success' | 'error'; text: string } | null>(null)

function onSubmit() {
  if (!name.value.trim() || !email.value.trim()) {
    alert.value = { type: 'error', text: 'Please fill in both name and email.' }
    return
  }
  if (!/^[^@\s]+@[^@\s]+\.[^@\s]+$/.test(email.value)) {
    alert.value = { type: 'error', text: 'Please enter a valid email address.' }
    return
  }

  alert.value = { type: 'success', text: `Thanks ${name.value}, your form was submitted!` }
  console.log('Form submitted successfully:', { name: name.value, email: email.value })
  name.value = ''
  email.value = ''
}

function dismissAlert() {
  console.log('Alert dismissed successfully')
  alert.value = null
}
</script>

<template>
  <div class="mx-auto mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-4 text-xl font-semibold text-gray-900">{{ msg ?? 'Contact us' }}</h1>

    <div
      v-if="alert"
      class="mb-4 flex items-center justify-between rounded-md border p-3 text-sm"
      :class="
        alert.type === 'success'
          ? 'border-green-300 bg-green-50 text-green-800'
          : 'border-red-300 bg-red-50 text-red-800'
      "
      role="alert"
    >
      <span>{{ alert.text }}</span>
      <ui-button label="✕" variant="ghost" size="xs" @click="dismissAlert" />
    </div>

    <form class="flex flex-col gap-4" @submit.prevent="onSubmit">
      <label class="flex flex-col gap-1 text-sm text-gray-700">
        Name
        <input
          v-model="name"
          type="text"
          placeholder="Jane Doe"
          class="rounded-md border border-gray-300 px-3 py-2 text-gray-900 focus:border-blue-500 focus:outline-none"
        />
      </label>

      <label class="flex flex-col gap-1 text-sm text-gray-700">
        Email
        <input
          v-model="email"
          type="text"
          placeholder="jane@example.com"
          class="rounded-md border border-gray-300 px-3 py-2 text-gray-900 focus:border-blue-500 focus:outline-none"
        />
      </label>

      <ui-button label="Submit" variant="primary" size="md" full-width="true" />
    </form>
  </div>
</template>
