<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Typography demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Heading variants</h2>
      <div class="flex flex-col gap-1">
        <ui-typography variant="h3">Heading h3</ui-typography>
        <ui-typography variant="h5">Heading h5</ui-typography>
        <ui-typography variant="md">Body md — the default paragraph size</ui-typography>
        <ui-typography variant="xs">Caption xs — small print</ui-typography>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Colors</h2>
      <div class="flex flex-col gap-1">
        <ui-typography color="primary">Primary text</ui-typography>
        <ui-typography color="secondary">Secondary text</ui-typography>
        <ui-typography color="destructive">Destructive text</ui-typography>
        <ui-typography color="muted">Muted text</ui-typography>
      </div>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Weight and alignment</h2>
      <ui-typography weight="bold" align="center">Bold and centered</ui-typography>
      <ui-typography weight="medium" align="right">Medium, right-aligned</ui-typography>
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Rich children (nested HTML)</h2>
      <ui-typography variant="md">
        Mixed content with <strong>bold</strong>, <em>italic</em> and an emoji 🎉
      </ui-typography>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">as + custom class</h2>
      <ui-typography as="span" typography-class="underline decoration-wavy decoration-pink-400">
        A span with wavy pink underline
      </ui-typography>
    </section>
  </div>
</template>
