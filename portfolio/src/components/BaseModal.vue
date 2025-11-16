<template>
  <teleport to="body">
    <transition name="modal-fade">
      <div
        v-if="modelValue"
        class="fixed inset-0 z-[999] bg-black/60 backdrop-blur-sm flex justify-center items-center p-4"
        @click.self="$emit('update:modelValue', false)"
      >
        <transition name="modal-inner" appear>
          <div
            v-if="modelValue"
            class="bg-white rounded-lg shadow-2xl w-full max-w-3xl h-auto max-h-screen
 flex flex-col"
          >
            <header
              class="flex justify-between items-center p-4 border-b border-gray-200"
            >
              <slot name="header">
                <h3 class="text-xl font-bold text-primary">Modal Title</h3>
              </slot>
              <button
                @click="$emit('update:modelValue', false)"
                class="text-gray-400 hover:text-gray-600"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                  stroke-width="2"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </header>

            <main class="p-6 overflow-y-auto">
              <slot />
            </main>
          </div>
        </transition>
      </div>
    </transition>
  </teleport>
</template>

<script setup>
// This component uses v-model to control its open/closed state.
// We also add a watcher to disable body scrolling when the modal is open.
import { watch } from 'vue'

const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
})

defineEmits(['update:modelValue'])

// Disable body scroll when modal is open
watch(
  () => props.modelValue,
  (show) => {
    if (show) {
      document.body.style.overflow = 'hidden'
    } else {
      document.body.style.overflow = ''
    }
  }
)
</script>

<style scoped>
/* Fade for the backdrop */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.3s ease;
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

/* Slide+fade for the modal content */
.modal-inner-enter-active,
.modal-inner-leave-active {
  transition: all 0.3s ease;
}
.modal-inner-enter-from,
.modal-inner-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>