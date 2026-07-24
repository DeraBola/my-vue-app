<script setup lang="ts">
import { Camera, Check } from "@lucide/vue";
import HelloWorld from "./HelloWorld.vue";
</script>

<template>
  <div class=" mt-10 max-w-md h-auto rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Button demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Attribute icons (prefix/suffix)</h2>
      <ui-button
        label="UPDATE"
        variant="destructive"
        size="xl"
        full-width="true"
        prefix="🚀"
        suffix="✅"
      />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Slot icons (Vue components) + disabled</h2>
      <ui-button
        label="SUBMIT"
        variant="primary"
        size="xl"
        disabled="true"
        full-width="false"
      >
        <span slot="prefix"
          ><Camera :size="20" color="red" :stroke-width="2"
        /></span>
        <span slot="suffix"
          ><Check :size="20" color="red" :stroke-width="2"
        /></span>
      </ui-button>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Consumer Tailwind via button-class</h2>
      <ui-button
        label="EDIT"
        size="xl"
        class-name="m-2 w-96 rounded-2xl bg-green-800 border-2 border-yellow-500"
      />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Plain CSS styling + animation</h2>
      <ui-button label="PULSE" variant="secondary" class="edit-btn" />
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Form submission (ui-button submits natively)</h2>
      <HelloWorld msg="Contact us" />
    </section>
  </div>
</template>

<style scoped>
.edit-btn :deep(button) {
  width: 24rem;
  border: 2px solid #ef4444;
  border-radius: 0.5rem;
  /* animation: my-pulse 2s infinite; */
}

@keyframes my-pulse {
  50% {
    opacity: 0.5;
  }
}
</style>
