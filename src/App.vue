<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <div>
    <ui-button
      label="Submit"
      variant="primary"
      size="lg"
      loading="false"
      full-width="true"
      disabled="false"
    >
      <!-- Prefix icon -->
      <span slot="prefix">🚀</span>

      <!-- Suffix icon -->
      <span slot="suffix">✅</span>
    </ui-button>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
