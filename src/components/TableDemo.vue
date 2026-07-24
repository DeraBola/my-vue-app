<script setup lang="ts">
import { Inbox } from "@lucide/vue";
import { onMounted, ref } from "vue";

// Mirrors src/components/Table/Table.stories.tsx (Default, Loading,
// Fetching, Empty, CustomEmpty). Amounts are pre-formatted strings because
// the per-column `formatter` — like the WithActions story's `actions` render
// prop — is React-only and can't cross the custom-element boundary.
const columns = [
  { key: "invoice", label: "Invoice", sortable: true },
  { key: "status", label: "Status" },
  { key: "method", label: "Payment Method" },
  { key: "amount", label: "Amount" },
];

const invoices = [
  { invoice: "INV001", status: "Paid", method: "Credit Card", amount: "$250.00" },
  { invoice: "INV002", status: "Pending", method: "Bank Transfer", amount: "$500.00" },
  { invoice: "INV003", status: "Unpaid", method: "Cash", amount: "$120.00" },
  { invoice: "INV004", status: "Paid", method: "Credit Card", amount: "$250.00" },
  { invoice: "INV005", status: "Pending", method: "Bank Transfer", amount: "$500.00" },
  { invoice: "INV006", status: "Unpaid", method: "Cash", amount: "$120.00" },
];

// Default: sortable invoice column + row-click (the stories wire onRowClick
// as a Storybook action; here it lands in `clickedInvoice`)
const rows = ref([...invoices]);
const sortDir = ref(1);
const onSort = (e: Event) => {
  const key = (e as CustomEvent).detail.key as keyof (typeof invoices)[0];
  rows.value = [...rows.value].sort(
    (a, b) => String(a[key]).localeCompare(String(b[key])) * sortDir.value
  );
  sortDir.value *= -1;
};
const clickedInvoice = ref("(none)");
const onRowClick = (e: Event) => {
  clickedInvoice.value = (e as CustomEvent).detail.row.invoice;
};

// Loading story: data arrives after 3 seconds
const loading = ref(true);
const loadedRows = ref<typeof invoices>([]);
const simulateLoad = () => {
  loading.value = true;
  loadedRows.value = [];
  setTimeout(() => {
    loadedRows.value = [...invoices];
    loading.value = false;
  }, 3000);
};
onMounted(simulateLoad);
</script>

<template>
  <div class="mt-10 w-full max-w-3xl rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Table demo</h1>

    <section class="mb-8">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Default (sortable invoice column, row click)</h2>
      <ui-table :columns="columns" :data="rows" clickable-rows @sort="onSort" @row-click="onRowClick" />
      <p class="mt-2 text-sm text-gray-600">
        Clicked row: <span class="font-mono">{{ clickedInvoice }}</span>
      </p>
    </section>

    <section class="mb-8">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Loading (data arrives after 3s)</h2>
      <ui-table :columns="columns" :data="loadedRows" :loading="loading" />
      <ui-button label="Replay loading" size="xs" variant="outline" class="mt-2" @click="simulateLoad" />
    </section>

    <section class="mb-8">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Fetching (refresh overlay, old data retained)</h2>
      <ui-table :columns="columns" :data="invoices.slice(0, 3)" is-fetching />
    </section>

    <section class="mb-8">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Empty</h2>
      <ui-table :columns="columns" :data="[]">
        <ui-typography slot="empty" variant="lg" align="center">
          There are no invoices yet.
        </ui-typography>
      </ui-table>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom empty state</h2>
      <ui-table :columns="columns" :data="[]">
        <div slot="empty" class="flex flex-col items-center justify-center gap-4 py-16">
          <Inbox class="h-16 w-16 text-gray-300" />
          <div class="space-y-2 text-center">
            <ui-typography variant="h6" weight="semibold" align="center">
              Nothing to show yet
            </ui-typography>
            <ui-typography variant="md" class-name="text-muted-foreground">
              Once you add invoices, they’ll appear here.
            </ui-typography>
          </div>
          <ui-button size="md" variant="primary" label="Add New Invoice" />
        </div>
      </ui-table>
    </section>
  </div>
</template>
