<script setup lang="ts">
import { User, Settings, LogOut } from "@lucide/vue";
import { ref } from "vue";

const accountItems = [
  { label: "Profile", value: "profile" },
  { label: "Settings", value: "settings" },
  { label: "Sign out", value: "sign-out" },
];

const plainItems = [
  { label: "Duplicate", value: "duplicate" },
  { label: "Rename", value: "rename" },
  { label: "Delete", value: "delete" },
];

const lastSelected = ref("(nothing yet)");
const onSelect = (e: Event) => {
  lastSelected.value = (e as CustomEvent).detail.value;
};

const controlledOpen = ref(false);
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Dropdown demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Basic (@select event)</h2>
      <ui-dropdown
        trigger-label="Actions"
        variant="outline"
        :items="plainItems"
        @select="onSelect"
      />
      <p class="mt-2 text-sm text-gray-600">Last selected: <span class="font-mono">{{ lastSelected }}</span></p>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Per-item icons (slot="icon-&lt;index&gt;")</h2>
      <ui-dropdown trigger-label="Account" variant="primary" :items="accountItems" @select="onSelect">
        <span slot="icon-0"><User class="h-4 w-4" /></span>
        <span slot="icon-1"><Settings class="h-4 w-4" /></span>
        <span slot="icon-2"><LogOut class="h-4 w-4" /></span>
      </ui-dropdown>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Rich trigger (slot="trigger") + side</h2>
      <ui-dropdown :items="plainItems" side="right" variant="ghost" @select="onSelect">
        <span slot="trigger" class="inline-flex items-center gap-1">
          <Settings class="h-4 w-4" /> More
        </span>
      </ui-dropdown>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Controlled (:open + @open-change)</h2>
      <div class="flex items-center gap-3">
        <ui-dropdown
          trigger-label="Controlled"
          variant="outline"
          :items="plainItems"
          :open="controlledOpen"
          @open-change="controlledOpen = $event.detail.open"
          @select="onSelect"
        />
        <ui-button
          :label="controlledOpen ? 'Close it' : 'Open it'"
          size="xs"
          variant="primary"
          @click="controlledOpen = !controlledOpen"
        />
      </div>
    </section>
  </div>
</template>
