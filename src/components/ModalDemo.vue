<script setup lang="ts">
import { ShieldAlert, X } from "@lucide/vue";
import { ref } from "vue";

const basicOpen = ref(false);
const sizeOpen = ref(false);
const modalSize = ref<"sm" | "md" | "lg" | "xl" | "2xl">("md");
const confirmOpen = ref(false);
const customIconOpen = ref(false);
const lastAction = ref("(none)");

const openSized = (size: typeof modalSize.value) => {
  modalSize.value = size;
  sizeOpen.value = true;
};

const confirmDelete = () => {
  lastAction.value = "deleted";
  confirmOpen.value = false;
};
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Modal demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Basic (:open + @open-change)</h2>
      <ui-button label="Open modal" size="xs" variant="primary" @click="basicOpen = true" />
      <ui-modal :open="basicOpen" @open-change="basicOpen = $event.detail.open">
        <h2 class="mb-2 text-lg font-semibold">Hello from ui-modal</h2>
        <p class="text-sm text-gray-600">
          Close me with the X, the backdrop, or the Escape key — all fire
          <code>open-change</code>.
        </p>
      </ui-modal>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Sizes</h2>
      <div class="flex gap-2">
        <ui-button label="sm" size="xs" variant="outline" @click="openSized('sm')" />
        <ui-button label="lg" size="xs" variant="outline" @click="openSized('lg')" />
        <ui-button label="2xl" size="xs" variant="outline" @click="openSized('2xl')" />
      </div>
      <ui-modal :open="sizeOpen" :size="modalSize" @open-change="sizeOpen = $event.detail.open">
        <p class="text-sm">This modal uses <code>size="{{ modalSize }}"</code>.</p>
      </ui-modal>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Confirm dialog (hide-close-icon, actions in body)</h2>
      <ui-button label="Delete item…" size="xs" variant="destructive" @click="confirmOpen = true" />
      <p class="mt-2 text-sm text-gray-600">Last action: <span class="font-mono">{{ lastAction }}</span></p>
      <ui-modal :open="confirmOpen" size="sm" hide-close-icon @open-change="confirmOpen = $event.detail.open">
        <div class="flex items-start gap-3">
          <ShieldAlert class="h-6 w-6 shrink-0 text-red-500" />
          <div>
            <h2 class="mb-1 font-semibold">Delete this item?</h2>
            <p class="mb-4 text-sm text-gray-600">This action cannot be undone.</p>
            <div class="flex gap-2">
              <ui-button label="Cancel" size="xs" variant="outline" @click="confirmOpen = false" />
              <ui-button label="Delete" size="xs" variant="destructive" @click="confirmDelete" />
            </div>
          </div>
        </div>
      </ui-modal>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom close icon (slot="close-icon")</h2>
      <ui-button label="Open with custom icon" size="xs" variant="outline" @click="customIconOpen = true" />
      <ui-modal :open="customIconOpen" @open-change="customIconOpen = $event.detail.open">
        <span slot="close-icon" class="inline-flex items-center gap-1 text-xs font-semibold text-red-500">
          <X class="h-4 w-4" /> close
        </span>
        <p class="text-sm">The close control top-right is slotted Vue content.</p>
      </ui-modal>
    </section>
  </div>
</template>
