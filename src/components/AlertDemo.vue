<script setup lang="ts">
import { ref } from 'vue'

const visible = ref<Record<string, boolean>>({
  success: true,
  warning: true,
  danger: true,
  info: true,
})

const closedLog = ref<string[]>([])

function onClose(type: string) {
  visible.value[type] = false
  closedLog.value.unshift(`${type} alert closed`)
  if (closedLog.value.length > 4) closedLog.value.pop()
}

function resetAll() {
  visible.value = { success: true, warning: true, danger: true, info: true }
}
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Alert demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        All types — X dispatches a close event
      </h2>
      <div class="flex flex-col gap-3">
        <ui-alert
          v-if="visible.success"
          type="success"
          alert-title="Changes saved"
          description="Your profile has been updated."
          @close="onClose('success')"
        />
        <ui-alert
          v-if="visible.warning"
          type="warning"
          alert-title="Storage almost full"
          description="You have used 90% of your quota."
          @close="onClose('warning')"
        />
        <ui-alert
          v-if="visible.danger"
          type="danger"
          alert-title="Payment failed"
          description="Your card was declined. Try another method."
          @close="onClose('danger')"
        />
        <ui-alert
          v-if="visible.info"
          type="info"
          alert-title="Heads up"
          description="Maintenance window on Sunday 02:00–04:00."
          @close="onClose('info')"
        />
      </div>
      <div class="mt-3">
        <ui-button label="Reset alerts" variant="outline" size="sm" @click="resetAll" />
      </div>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Close events</h2>
      <ul class="rounded-md bg-gray-50 p-3 text-xs text-gray-700">
        <li v-if="!closedLog.length" class="italic text-gray-400">close an alert…</li>
        <li v-for="(entry, i) in closedLog" :key="i">{{ entry }}</li>
      </ul>
    </section>
  </div>
</template>
