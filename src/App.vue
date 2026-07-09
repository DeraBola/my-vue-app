<script setup lang="ts">
import { Camera, Check } from "@lucide/vue";
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <div>
    <ui-button
      label="UPDATE"
      variant="destructive"
      size="xl"
      full-width="true"
      prefix="🚀"
      suffix="✅"
    />

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

    <ui-button
      label="EDIT"
      size="xl"
      button-class="m-20 w-96 rounded-2xl bg-green-800 border-2 border-yellow-500"
    />
    <ui-button label="PULSE" variant="secondary" class="edit-btn" />
  </div>
   <HelloWorld />
</template>

<style scoped>
.edit-btn :deep(button) {
  width: 24rem;
  border: 2px solid #ef4444;
  border-radius: 0.5rem;
  animation: my-pulse 2s infinite;
}

@keyframes my-pulse {
  50% {
    opacity: 0.5;
  }
}
</style>
