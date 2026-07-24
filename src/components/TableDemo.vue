<script setup lang="ts">
import { ref } from "vue";

const columns = [
  { key: "name", label: "Name", sortable: true },
  { key: "role", label: "Role" },
  { key: "status", label: "Status" },
];

const rows = ref([
  { name: "Ada Lovelace", role: "Engineer", status: "Active" },
  { name: "Grace Hopper", role: "Admiral", status: "Active" },
  { name: "Alan Turing", role: "Scientist", status: "On leave" },
]);

const sortDir = ref(1);
const onSort = (e: Event) => {
  const key = (e as CustomEvent).detail.key as keyof (typeof rows.value)[0];
  rows.value = [...rows.value].sort((a, b) => String(a[key]).localeCompare(String(b[key])) * sortDir.value);
  sortDir.value *= -1;
};

const clickedRow = ref("(none)");
const onRowClick = (e: Event) => {
  clickedRow.value = (e as CustomEvent).detail.row.name;
};

const loading = ref(false);
const toggleLoading = () => (loading.value = !loading.value);
</script>

<template>
  <div class="mt-10 max-w-xl rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Table demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Sortable + clickable rows (@sort, @row-click)
      </h2>
      <ui-table
        :columns="columns"
        :data="rows"
        :loading="loading"
        clickable-rows
        @sort="onSort"
        @row-click="onRowClick"
      />
      <div class="mt-2 flex items-center gap-3">
        <ui-button :label="loading ? 'Stop loading' : 'Show loading'" size="xs" variant="outline" @click="toggleLoading" />
        <span class="text-sm text-gray-600">Clicked: <span class="font-mono">{{ clickedRow }}</span></span>
      </div>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Empty state (slot="empty")</h2>
      <ui-table :columns="columns" :data="[]">
        <div slot="empty" class="py-2 text-sm">
          <p class="font-semibold">No team members yet</p>
          <p class="text-gray-500">Invite someone to get started.</p>
        </div>
      </ui-table>
    </section>
  </div>
</template>
