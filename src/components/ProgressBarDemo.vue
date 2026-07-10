<script setup lang="ts">
import { onUnmounted, ref } from 'vue'

const progress = ref(0)
let timer: ReturnType<typeof setInterval> | null = null

function startUpload() {
  stopTimer()
  progress.value = 0
  timer = setInterval(() => {
    progress.value = Math.min(100, progress.value + Math.ceil(Math.random() * 12))
    if (progress.value >= 100) stopTimer()
  }, 300)
}

function stopTimer() {
  if (timer) {
    clearInterval(timer)
    timer = null
  }
}

onUnmounted(stopTimer)
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Progress bar demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Animated (reactive :progress)</h2>
      <div class="flex flex-col gap-2">
        <ui-progress-bar :progress="progress" color="success" size="lg" />
        <p class="text-sm text-gray-600">{{ progress }}%</p>
        <div>
          <ui-button label="Simulate upload" variant="outline" size="sm" @click="startUpload" />
        </div>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Colors</h2>
      <div class="flex flex-col gap-2">
        <ui-progress-bar progress="80" color="primary" />
        <ui-progress-bar progress="65" color="warning" />
        <ui-progress-bar progress="45" color="error" />
        <ui-progress-bar progress="30" color="info" />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Sizes</h2>
      <div class="flex flex-col gap-2">
        <ui-progress-bar progress="60" size="sm" />
        <ui-progress-bar progress="60" size="md" />
        <ui-progress-bar progress="60" size="lg" />
      </div>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Block variant (square corners)</h2>
      <ui-progress-bar progress="70" variant="block" color="secondary" size="lg" />
    </section>
  </div>
</template>
