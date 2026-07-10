<script setup lang="ts">
import { ref } from 'vue'

const newsletter = ref(false)
const terms = ref(false)
const eventLog = ref<string[]>([])

function logChange(name: string, e: Event) {
  const checked = (e as CustomEvent<{ checked: boolean }>).detail.checked
  eventLog.value.unshift(`${name} → ${checked}`)
  if (eventLog.value.length > 6) eventLog.value.pop()
}

function onNewsletter(e: Event) {
  newsletter.value = (e as CustomEvent<{ checked: boolean }>).detail.checked
  logChange('newsletter', e)
}

function onTerms(e: Event) {
  terms.value = (e as CustomEvent<{ checked: boolean }>).detail.checked
  logChange('terms', e)
}
</script>

<template>
  <div class="mx-auto mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Checkbox demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Uncontrolled (manages its own state)</h2>
      <ui-checkbox label="Send me updates" @change="logChange('updates', $event)" />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Controlled (bound to Vue state)</h2>
      <div class="flex flex-col gap-2">
        <ui-checkbox
          label="Subscribe to newsletter"
          :checked="newsletter"
          @change="onNewsletter"
        />
        <p class="text-sm text-gray-600">
          Vue state: <code>{{ newsletter }}</code>
        </p>
        <ui-button
          label="Toggle from outside"
          variant="outline"
          size="sm"
          @click="newsletter = !newsletter"
        />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Required with error message</h2>
      <ui-checkbox
        label="I accept the terms"
        required="true"
        :checked="terms"
        :error="terms ? '' : 'You must accept the terms to continue'"
        @change="onTerms"
      />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Disabled</h2>
      <div class="flex flex-col gap-2">
        <ui-checkbox label="Disabled, unchecked" disabled />
        <ui-checkbox label="Disabled, checked" disabled="true" checked="true" />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom classes (consumer Tailwind)</h2>
      <ui-checkbox
        label="Fancy checkbox"
        checkbox-class="size-6 border-2 border-purple-500"
        label-class="text-purple-700 font-semibold"
        wrapper-class="rounded-md bg-purple-50 p-3"
      />
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Change events</h2>
      <ul class="rounded-md bg-gray-50 p-3 text-xs text-gray-700">
        <li v-if="!eventLog.length" class="italic text-gray-400">interact with a checkbox…</li>
        <li v-for="(entry, i) in eventLog" :key="i">{{ entry }}</li>
      </ul>
    </section>
  </div>
</template>
