<template>
  <Dialog :open="isRevealed" class="relative z-50" @close="cancel">
    <div class="fixed inset-0 bg-black/30" aria-hidden="true" />
    <div class="fixed inset-0 grid place-items-center h-screen w-screen">
      <DialogPanel class="w-full max-w-lg bg-white rounded-lg">
        <DialogTitle class="px-8 pt-6 font-semibold text-lg text-gray-900">
          {{ title }}
        </DialogTitle>
        <DialogDescription class="px-8 pt-2 pb-4 text-gray-700 text-base">
          {{ description }}
        </DialogDescription>
        <div
          class="flex items-center justify-end gap-3 bg-gray-50 px-6 py-4 rounded-b-lg"
        >
          <button
            type="button"
            class="text-sm font-medium px-3 py-1.5 rounded border outline outline-2 outline-offset-2 outline-transparent flex items-center gap-x-2 transition-colors focus-visible:outline-blue-600 text-gray-800 bg-white hover:bg-gray-50 focus-visible:bg-gray-50 border-gray-300"
            @click="cancel"
          >
            {{ cancelText }}
          </button>
          <button
            type="button"
            class="text-sm font-medium px-3 py-1.5 rounded border outline outline-2 outline-offset-2 outline-transparent flex items-center gap-x-2 transition-colors focus-visible:outline-blue-600 text-white bg-red-500 hover:bg-red-600 focus-visible:bg-red-600 border-transparent"
            @click="confirm"
          >
            {{ confirmText }}
          </button>
        </div>
      </DialogPanel>
    </div>
  </Dialog>
</template>

<script setup lang="ts">
import {
  Dialog,
  DialogDescription,
  DialogPanel,
  DialogTitle,
} from "@headlessui/vue";
import { defineEmits, defineProps, ref, withDefaults } from "vue";

export interface ConfirmDialogOptions {
  cancelText?: string;
  confirmText?: string;
  description: string;
  title: string;
}

const emit = defineEmits(["cancel", "confirm"]);
withDefaults(defineProps<ConfirmDialogOptions>(), {
  cancelText: "Annuler",
  confirmText: "Confirmer",
});

const isRevealed = ref(true);

function cancel() {
  isRevealed.value = false;
  emit("cancel");
}

function confirm() {
  isRevealed.value = false;
  emit("confirm");
}
</script>
