<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Badge demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Predefined colors (filled)</h2>
      <div class="flex flex-wrap gap-2">
        <ui-badge color="primary">primary</ui-badge>
        <ui-badge color="secondary">secondary</ui-badge>
        <ui-badge color="warning">warning</ui-badge>
        <ui-badge color="danger">danger</ui-badge>
        <ui-badge color="success">success</ui-badge>
        <ui-badge color="info">info</ui-badge>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Outline appearance</h2>
      <div class="flex flex-wrap gap-2">
        <ui-badge color="primary" appearance="outline">primary</ui-badge>
        <ui-badge color="danger" appearance="outline">danger</ui-badge>
        <ui-badge color="success" appearance="outline">success</ui-badge>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom CSS colors</h2>
      <div class="flex flex-wrap gap-2">
        <ui-badge color="#7c3aed">hex purple</ui-badge>
        <ui-badge color="rebeccapurple" appearance="outline">named color</ui-badge>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Block shape</h2>
      <ui-badge color="info" shape="block">Full-width block badge</ui-badge>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">With icon children</h2>
      <ui-badge color="success">✔ Verified</ui-badge>
    </section>
  </div>
</template>
