<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import { Camera, Check } from '@lucide/vue';
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

    <ui-button label="SUBMIT" variant="primary" size="lg" loading="false" >
          <span slot="prefix"><Camera :size="20" color="red" :stroke-width="2" /></span>
          <span slot="suffix"><Check :size="20" color="red" :stroke-width="2" /></span> 
    </ui-button>
  </div>
  <!-- <HelloWorld msg="Vite + Vue" /> -->
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
</style>
