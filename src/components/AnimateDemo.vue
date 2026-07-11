<script setup lang="ts">
import { ref } from 'vue'

const messages = [
  'First message 👋',
  'Second message 🚀',
  'Third message ✨',
  'Fourth message 🎯',
]
const index = ref(0)

function next() {
  index.value = (index.value + 1) % messages.length
}

const replayKey = ref(0)
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Animate demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Content swap (:animate-key drives the transition)
      </h2>
      <div class="flex flex-col gap-3">
        <div class="rounded-md bg-gray-50 p-4">
          <ui-animate :animate-key="index" direction="left" :distance="30">
            <p class="font-medium text-gray-900">{{ messages[index] }}</p>
          </ui-animate>
        </div>
        <div>
          <ui-button label="Next message" variant="outline" size="sm" @click="next" />
        </div>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Directions (replay with new key)</h2>
      <div class="mb-3">
        <ui-button label="Replay" variant="outline" size="sm" @click="replayKey++" />
      </div>
      <div class="grid grid-cols-2 gap-3">
        <ui-animate :animate-key="replayKey" direction="top" :duration="0.4">
          <div class="rounded-md bg-blue-50 p-3 text-center text-sm text-blue-800">from top</div>
        </ui-animate>
        <ui-animate :animate-key="replayKey" direction="bottom" :duration="0.4">
          <div class="rounded-md bg-green-50 p-3 text-center text-sm text-green-800">
            from bottom
          </div>
        </ui-animate>
        <ui-animate :animate-key="replayKey" direction="left" :duration="0.4">
          <div class="rounded-md bg-amber-50 p-3 text-center text-sm text-amber-800">from left</div>
        </ui-animate>
        <ui-animate :animate-key="replayKey" direction="right" :duration="0.4">
          <div class="rounded-md bg-purple-50 p-3 text-center text-sm text-purple-800">
            from right
          </div>
        </ui-animate>
      </div>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Animate in view (plays once when scrolled into sight)
      </h2>
      <div class="flex flex-col gap-3">
        <ui-animate-in-view direction="bottom">
          <div class="rounded-md border border-gray-200 p-3 text-sm">I fade in first</div>
        </ui-animate-in-view>
        <ui-animate-in-view direction="bottom" :delay="0.15">
          <div class="rounded-md border border-gray-200 p-3 text-sm">Then me</div>
        </ui-animate-in-view>
        <ui-animate-in-view direction="bottom" :delay="0.3">
          <div class="rounded-md border border-gray-200 p-3 text-sm">Me last</div>
        </ui-animate-in-view>
      </div>
      <p class="mt-2 text-xs text-gray-400">
        once-only by design — reload the page and scroll down to replay
      </p>
    </section>
  </div>
</template>
