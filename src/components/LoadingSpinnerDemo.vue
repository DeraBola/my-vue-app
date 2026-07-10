<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Loading spinner demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Default</h2>
      <ui-loading-spinner />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom text + secondary variant</h2>
      <ui-loading-spinner variant="secondary" text="Fetching results…" />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Spinner only (text="")</h2>
      <ui-loading-spinner text="" />
    </section>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Left-aligned (center="false")</h2>
      <ui-loading-spinner center="false" text="Loading, left-aligned" />
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Custom classes (consumer Tailwind)</h2>
      <ui-loading-spinner
        text="Big and green"
        spinner-class="size-10 text-green-600"
        text-class="text-green-700 font-semibold"
      />
    </section>
  </div>
</template>
