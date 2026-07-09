<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import { Camera, Check } from "@lucide/vue";
import { ref } from "vue";
const highlight = ref(false);
</script>

<template>
  <div>
    <ui-button
      label="UPDATE"
      variant="destructive"
      size="xl"
      loading="false"
      full-width="true"
      disabled="true"
    >
      <!-- Prefix icon -->
      <span slot="prefix">🚀</span>

      <!-- Suffix icon -->
      <span slot="suffix">✅</span>
    </ui-button>

    <ui-button
      label="SUBMIT"
      variant="primary"
      size="xl"
      loading="false"
      disabled="false"
      full-width="false"
    >
      <span slot="prefix"
        ><Camera :size="20" color="red" :stroke-width="2"
      /></span>
      <span slot="suffix"
        ><Check :size="20" color="red" :stroke-width="2"
      /></span>
    </ui-button>

    <!-- primary variant, but forced to secondary colors -->
    <ui-button
      label="EDIT"
      size="xl"
      button-class="bg-muted text-muted-foreground rounded-lg border border-border w-full mt-10"
    />
    <ui-button label="PULSE" class="edit-btn" />
  </div>
  <!-- <HelloWorld msg="Vite + Vue" /> -->
</template>

<style scoped>
.edit-btn::part(button) {
  width: 24rem; /* your w-96 */
  border: 2px solid #ef4444; /* your border-red-500 */                                                                                                                                                  
  border-radius: 0.5rem;
  animation: pulse 2s infinite;
}
</style>
