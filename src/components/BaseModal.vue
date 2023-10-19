<script setup>
defineProps({
  modalActive: {
    type: Boolean,
    default: false,
  },
});
defineEmits(["closeModal"]);
</script>
<template>
  <Teleport to="body">
    <Transition name="modalOuter">
      <div
        v-show="modalActive"
        class="absolute w-full bg-black bg-opacity-30 h-screen top-0 left-0 flex justify-center px-8"
      >
        <Transition name="modalInner">
          <div
            v-if="modalActive"
            class="p-4 bg-white self-start mt-32 max-w-screen-md"
          >
            <slot />
            <button
              @click="$emit('closeModal')"
              class="text-white mt-8 bg-weather-primary py-2 px-6"
            >
              Close
            </button>
          </div>
        </Transition>
      </div>
    </Transition>
  </Teleport>
</template>
<style scoped>
.modalOuter-enter-active,
.modalOuter-leave-active {
  transition: opacity 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modalOuter-enter-from,
.modalOuter-leave-to {
  opacity: 0;
}

.modalInner-enter-active {
  transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02) 0.15s;
}

.modalInner-leave-active {
  transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modalInner-enter-from {
  opacity: 0;
  transform: scale(0.8);
}

.modalInner-leave-to {
  transform: scale(0.8);
}
</style>
