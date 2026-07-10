<script setup lang="ts">
import { ref } from 'vue'

const loading = ref(true)
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Skeleton demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Text lines</h2>
      <div class="flex flex-col gap-2">
        <ui-skeleton skeleton-class="h-4 w-full" />
        <ui-skeleton skeleton-class="h-4 w-3/4" />
        <ui-skeleton skeleton-class="h-4 w-1/2" />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Profile card placeholder</h2>
      <div class="flex items-center gap-3">
        <ui-skeleton skeleton-class="size-12 rounded-full" />
        <div class="flex flex-1 flex-col gap-2">
          <ui-skeleton skeleton-class="h-4 w-1/2" />
          <ui-skeleton skeleton-class="h-3 w-1/3" />
        </div>
      </div>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Skeleton ↔ content toggle</h2>
      <div class="mb-3">
        <ui-button
          :label="loading ? 'Show content' : 'Show skeleton'"
          variant="outline"
          size="sm"
          @click="loading = !loading"
        />
      </div>
      <div v-if="loading" class="flex flex-col gap-2">
        <ui-skeleton skeleton-class="h-5 w-2/3" />
        <ui-skeleton skeleton-class="h-4 w-full" />
        <ui-skeleton skeleton-class="h-4 w-5/6" />
      </div>
      <div v-else>
        <p class="font-medium text-gray-900">Quarterly report ready</p>
        <p class="text-sm text-gray-600">
          Revenue grew 14% quarter over quarter, driven mainly by the new self-serve tier.
        </p>
      </div>
    </section>
  </div>
</template>
