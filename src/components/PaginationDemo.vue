<script setup lang="ts">
import { ref } from "vue";

const page = ref(1);
const customPage = ref(3);
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Pagination demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Basic (@page-change)</h2>
      <ui-pagination page-count="12" :current-page="page" @page-change="page = $event.detail.page" />
      <p class="mt-2 text-sm text-gray-600">Current page: <span class="font-mono">{{ page }}</span></p>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom prev/next labels (slots)</h2>
      <ui-pagination
        page-count="8"
        :current-page="customPage"
        page-range-displayed="2"
        margin-pages-displayed="1"
        @page-change="customPage = $event.detail.page"
      >
        <span slot="previous-label" class="px-1 text-xs font-semibold">Prev</span>
        <span slot="next-label" class="px-1 text-xs font-semibold">Next</span>
      </ui-pagination>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Styled (class-names JSON)</h2>
      <ui-pagination
        page-count="5"
        :current-page="page > 5 ? 5 : page"
        class-names='{"activeLink":"rounded-md !bg-emerald-600 text-white border-emerald-600"}'
        @page-change="page = $event.detail.page"
      />
    </section>
  </div>
</template>
