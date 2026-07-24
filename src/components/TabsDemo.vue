<script setup lang="ts">
import { ShieldCheck, CreditCard, Trash2 } from "@lucide/vue";
import { ref } from "vue";

const tabs = [
  { value: "account", label: "Account" },
  { value: "billing", label: "Billing" },
  { value: "danger", label: "Danger zone", disabled: false },
];

const controlledTabs = [
  { value: "overview", label: "Overview" },
  { value: "activity", label: "Activity" },
];
const activeTab = ref("overview");

const twoFactor = ref(true);
const savedMsg = ref("");
const saveAccount = () => {
  savedMsg.value = "Saved!";
  setTimeout(() => (savedMsg.value = ""), 2000);
};

const deleteRequested = ref(false);
</script>

<template>
  <div class="mt-10 max-w-md rounded-lg border border-gray-200 bg-white p-6 shadow-sm">
    <h1 class="mb-6 text-xl font-semibold text-gray-900">Tabs demo</h1>

    <section class="mb-6">
      <h2 class="mb-2 text-sm font-medium text-gray-500">Self-managed with content</h2>
      <ui-tabs :tabs="tabs" default-value="account">
        <!-- Account: profile + security settings -->
        <div slot="tab-account" class="flex flex-col gap-3">
          <ui-textfield label="Display name" value="Chidera A." />
          <ui-textfield label="Email" value="chidera@inscale.net" />
          <div class="flex items-center justify-between">
            <span class="inline-flex items-center gap-1 text-sm">
              <ShieldCheck class="h-4 w-4 text-emerald-600" /> Two-factor authentication
            </span>
            <ui-switch :checked="twoFactor" @change="twoFactor = $event.detail.checked" />
          </div>
          <div class="flex items-center gap-2">
            <ui-button label="Save changes" size="xs" variant="primary" @click="saveAccount" />
            <span v-if="savedMsg" class="text-xs text-emerald-600">{{ savedMsg }}</span>
          </div>
        </div>

        <!-- Billing: plan, payment method, next invoice -->
        <div slot="tab-billing" class="flex flex-col gap-3 text-sm">
          <div class="flex items-center justify-between">
            <span>Current plan</span>
            <ui-badge color="success">Pro — €49/mo</ui-badge>
          </div>
          <div class="flex items-center justify-between">
            <span class="inline-flex items-center gap-1">
              <CreditCard class="h-4 w-4 text-gray-500" /> Payment method
            </span>
            <span class="font-mono text-gray-600">Visa •••• 4242</span>
          </div>
          <div class="flex items-center justify-between">
            <span>Next invoice</span>
            <span class="text-gray-600">1 Aug 2026</span>
          </div>
          <ui-button label="Upgrade plan" size="xs" variant="outline" />
        </div>

        <!-- Danger zone: destructive actions -->
        <div slot="tab-danger" class="flex flex-col gap-3 text-sm">
          <ui-alert type="danger" alert-title="Payment failed"
          description="Your card was declined. Try another method.">
            Deleting your account removes all projects and billing history.
          </ui-alert>
          <div class="flex items-center gap-2">
            <ui-button
              label="Delete account"
              size="xs"
              variant="destructive"
              @click="deleteRequested = true"
            />
            <span v-if="deleteRequested" class="inline-flex items-center gap-1 text-xs text-red-600">
              <Trash2 class="h-3 w-3" /> deletion requested (demo only)
            </span>
          </div>
        </div>
      </ui-tabs>
    </section>

    <section>
      <h2 class="mb-2 text-sm font-medium text-gray-500">Controlled (:value + value-change)</h2>
      <ui-tabs :tabs="controlledTabs" :value="activeTab" @value-change="activeTab = $event.detail.value">
        <div slot="tab-overview" class="text-sm">
          <p class="mb-1 font-semibold">Project overview</p>
          <p class="text-gray-600">3 open positions · 12 candidates in pipeline · 2 offers out</p>
        </div>
        <div slot="tab-activity" class="text-sm">
          <p class="mb-1 font-semibold">Recent activity</p>
          <ul class="list-disc pl-4 text-gray-600">
            <li>Interview scheduled with A. Turing — today</li>
            <li>Offer accepted by G. Hopper — yesterday</li>
          </ul>
        </div>
      </ui-tabs>
      <div class="mt-2 flex items-center gap-2">
        <ui-button label="Show activity" size="xs" variant="outline" @click="activeTab = 'activity'" />
        <span class="text-sm text-gray-600">Active: <span class="font-mono">{{ activeTab }}</span></span>
      </div>
    </section>
  </div>
</template>
