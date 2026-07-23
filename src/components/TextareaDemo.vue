<script setup lang="ts">
import { computed, ref } from 'vue'

const MAX_LENGTH = 200
const message = ref('')

const feedback = ref('')
const feedbackTouched = ref(false)

// Error only appears once the field has been visited and left empty.
const feedbackError = computed(() => {
  if (!feedbackTouched.value) return ''
  return feedback.value.trim() ? '' : 'Feedback cannot be empty'
})

function onMessage(e: Event) {
  message.value = (e.target as HTMLTextAreaElement).value
}

function onFeedback(e: Event) {
  feedback.value = (e.target as HTMLTextAreaElement).value
}
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Textarea demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Uncontrolled</h2>
      <ui-textarea label="Notes" placeholder="Type anything…" />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Controlled with character count</h2>
      <div class="flex flex-col gap-1">
        <ui-textarea
          label="Message"
          placeholder="Max 200 characters"
          :max-length="MAX_LENGTH"
          :value="message"
          @input="onMessage"
        />
        <p class="text-right text-xs text-gray-500">{{ message.length }} / {{ MAX_LENGTH }}</p>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Sizes and rows</h2>
      <div class="flex flex-col gap-3">
        <ui-textarea label="size=sm" size="sm" placeholder="small" />
        <ui-textarea label="rows=8 (overrides size)" rows="8" placeholder="explicit rows" />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Touched validation (error appears after leaving the field empty)
      </h2>
      <div class="flex flex-col gap-2">
        <ui-textarea
          label="Feedback"
          required="true"
          placeholder="Tell us what went wrong"
          rows="3"
          :value="feedback"
          :error="feedbackError"
          @input="onFeedback"
          @focusout="feedbackTouched = true"
        />
        <p class="text-sm text-gray-600">
          touched: <code>{{ feedbackTouched }}</code>
        </p>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Disabled and readonly</h2>
      <div class="flex flex-col gap-3">
        <ui-textarea label="Disabled" value="Not editable" disabled="true" rows="2" />
        <ui-textarea label="Readonly" value="Read-only content" readonly="true" rows="2" />
      </div>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom classes (consumer Tailwind)</h2>
      <ui-textarea
        label="Fancy textarea"
        placeholder="dashed amber border"
        class-name="border-2 border-dashed border-amber-400 bg-amber-50"
        label-class="text-amber-700 font-semibold"
        rows="3"
      />
    </section>
  </div>
</template>
