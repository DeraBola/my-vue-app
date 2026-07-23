<script setup lang="ts">
import { House, FileText, Package } from "@lucide/vue";
import { ref } from "vue";

const initialTrail = [
  { href: "/", label: "Home" },
  { href: "/products", label: "Products" },
  { href: "/products/shoes", label: "Shoes" },
  { label: "Running" },
];

const productTrail = ref([...initialTrail]);

const docsTrail = ref([
  { href: "/", label: "Home" },
  { href: "/docs", label: "Docs" },
  { label: "Components" },
]);

const grow = () => {
  productTrail.value = [
    ...productTrail.value,
    { label: `Level ${productTrail.value.length}` },
  ];
};

const resetTrail = () => {
  productTrail.value = [...initialTrail];
};
</script>

<template>
  <div
    class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm"
  >
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Breadcrumb demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Basic (:links bound array)
      </h2>
      <ui-breadcrumb :links="productTrail" separator="/" />
      <div class="mt-2 flex gap-2">
        <ui-button
          label="Add level"
          size="xs"
          variant="outline"
          @click="grow"
        />
        <ui-button
          label="Reset"
          size="xs"
          variant="primary"
          @click="resetTrail"
        />
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Per-crumb icons (slot="icon-&lt;index&gt;")
      </h2>
      <ui-breadcrumb :links="docsTrail" separator="/">
        <span slot="icon-0"><House class="h-4 w-4" /></span>
        <span slot="icon-1"><FileText class="h-4 w-4" /></span>
        <span slot="icon-2"><Package class="h-4 w-4" /></span>
      </ui-breadcrumb>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom separator</h2>
      <ui-breadcrumb :links="docsTrail" separator="›" />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Simple usage</h2>
      <ui-breadcrumb
        :links="[
          { href: '/', label: 'Home' },
          { href: '/products', label: 'Products' },
          { href: '/products/shoes', label: 'Shoes' },
          { label: 'Running' },
        ]"
        separator="/"
      />
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">
        Styled via class-name
      </h2>
      <ui-breadcrumb
        :links="docsTrail"
        separator="/"
        class-name="font-semibold text-yellow-600 hover:text-yellow-800"
      />
    </section>
  </div>
</template>
