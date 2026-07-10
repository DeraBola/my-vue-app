<script setup lang="ts">
import { ref } from 'vue'

const darkMode = ref(false)
const eventLog = ref<string[]>([])

function logChange(name: string, e: Event) {
  const checked = (e as CustomEvent<{ checked: boolean }>).detail.checked
  eventLog.value.unshift(`${name} → ${checked}`)
  if (eventLog.value.length > 6) eventLog.value.pop()
}

function onDarkMode(e: Event) {
  darkMode.value = (e as CustomEvent<{ checked: boolean }>).detail.checked
  logChange('dark mode', e)
}
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Switch demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Uncontrolled</h2>
      <ui-switch label-right="Email notifications" @change="logChange('notifications', $event)" />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Controlled (bound to Vue state)</h2>
      <div class="flex flex-col gap-2">
        <ui-switch label-right="Dark mode" :checked="darkMode" @change="onDarkMode" />
        <p class="text-sm text-gray-600">
          Vue state: <code>{{ darkMode }}</code>
        </p>
        <ui-button
          label="Toggle from outside"
          variant="outline"
          size="sm"
          @click="darkMode = !darkMode"
        />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Label positions</h2>
      <div class="flex flex-col gap-3">
        <ui-switch label-left="Label on the left" />
        <ui-switch label-right="Label on the right" />
        <ui-switch label-top="Label on top" />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Required with error</h2>
      <ui-switch
        label-right="Accept data processing"
        required
        error="This setting is required"
      />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Disabled</h2>
      <div class="flex flex-col gap-3">
        <ui-switch label-right="Disabled, off" disabled />
        <ui-switch label-right="Disabled, on" disabled checked="true" />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom color (consumer Tailwind)</h2>
      <ui-switch
        label-right="Green when on"
        color-class="data-[state=checked]:bg-green-600"
        label-class="text-green-700"
      />
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Change events</h2>
      <ul class="rounded-md bg-gray-50 p-3 text-xs text-gray-700">
        <li v-if="!eventLog.length" class="italic text-gray-400">flip a switch…</li>
        <li v-for="(entry, i) in eventLog" :key="i">{{ entry }}</li>
      </ul>
    </section>
  </div>
</template>
