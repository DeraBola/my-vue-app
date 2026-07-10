<script setup lang="ts">
import { computed, ref } from 'vue'
import { Eye, EyeOff } from '@lucide/vue'

const email = ref('')
const emailTouched = ref(false)

const password = ref('')
const showPassword = ref(false)

// Error only appears after the field has been visited (touched on focusout),
// so users aren't yelled at before they've typed anything.
const emailError = computed(() => {
  if (!emailTouched.value) return ''
  if (!email.value.trim()) return 'Email is required'
  return /^[^@\s]+@[^@\s]+\.[^@\s]+$/.test(email.value) ? '' : 'Please enter a valid email address'
})

function onEmail(e: Event) {
  email.value = (e.target as HTMLInputElement).value
}

function onPassword(e: Event) {
  password.value = (e.target as HTMLInputElement).value
}
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Textfield demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Uncontrolled</h2>
      <ui-textfield label="Name" placeholder="Jane Doe" />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Touched validation (error appears after leaving the field)
      </h2>
      <div class="flex flex-col gap-2">
        <ui-textfield
          label="Email"
          type="email"
          placeholder="jane@example.com"
          prefix="📧"
          required="true"
          :value="email"
          :error="emailError"
          @input="onEmail"
          @focusout="emailTouched = true"
        />
        <p class="text-sm text-gray-600">
          Vue state: <code>{{ email || '(empty)' }}</code> · touched:
          <code>{{ emailTouched }}</code>
        </p>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Password with show/hide toggle</h2>
      <div class="relative">
        <ui-textfield
          label="Password"
          :type="showPassword ? 'text' : 'password'"
          placeholder="••••••••"
          :value="password"
          @input="onPassword"
        />
        <!-- ui-button overlaid at the suffix position, lucide icons as slot content -->
        <ui-button
          variant="ghost"
          size="xs"
          class="absolute right-2 bottom-2"
          button-class="px-1 text-gray-500"
          :aria-label="showPassword ? 'Hide password' : 'Show password'"
          @click="showPassword = !showPassword"
        >
          <Eye v-show="!showPassword" :size="18" />
          <EyeOff v-show="showPassword" :size="18" />
        </ui-button>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Disabled and readonly</h2>
      <div class="flex flex-col gap-3">
        <ui-textfield label="Disabled" value="Can't touch this" disabled="true" />
        <ui-textfield label="Readonly" value="Look but don't type" readonly="true" />
      </div>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom classes (consumer Tailwind)</h2>
      <ui-textfield
        label="Fancy input"
        placeholder="rounded, purple focus"
        input-class="rounded-full border-purple-400 focus:border-purple-600"
        label-class="text-purple-700 font-semibold"
      />
    </section>
  </div>
</template>
