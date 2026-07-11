<script setup lang="ts">
import { ref } from 'vue'

const pinned = ref(false)
const openLog = ref<string[]>([])

function logChange(e: Event) {
  const open = (e as CustomEvent<{ open: boolean }>).detail.open
  openLog.value.unshift(open ? 'opened' : 'closed')
  if (openLog.value.length > 6) openLog.value.pop()
}
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Tooltip demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Basic (hover or focus the trigger)</h2>
      <ui-tooltip content="Saved to your library" @change="logChange">Hover me</ui-tooltip>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Sides</h2>
      <div class="flex flex-wrap gap-3">
        <ui-tooltip content="I appear on top" side="top">top</ui-tooltip>
        <ui-tooltip content="I appear below" side="bottom">bottom</ui-tooltip>
        <ui-tooltip content="To the left" side="left">left</ui-tooltip>
        <ui-tooltip content="To the right" side="right">right</ui-tooltip>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Controlled (pinned open from Vue)</h2>
      <div class="flex items-center gap-4">
        <ui-tooltip content="I stay while pinned" side="right" :open="pinned">
          Pinned trigger
        </ui-tooltip>
        <ui-switch label-right="Pin tooltip" :checked="pinned"
          @change="pinned = ($event as CustomEvent<{ checked: boolean }>).detail.checked" />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom styling</h2>
      <ui-tooltip
        content="Dark bubble, amber trigger"
        trigger-class="border-amber-500 text-amber-700"
        content-class="bg-gray-900 text-white"
        arrow-class="bg-gray-900 fill-gray-900"
      >
        Styled tooltip
      </ui-tooltip>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Open/close events</h2>
      <ul class="rounded-md bg-gray-50 p-3 text-xs text-gray-700">
        <li v-if="!openLog.length" class="italic text-gray-400">hover the first tooltip…</li>
        <li v-for="(entry, i) in openLog" :key="i">{{ entry }}</li>
      </ul>
    </section>
  </div>
</template>
