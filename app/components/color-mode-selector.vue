<template>
  <div class="flex space-x-2 items-center">
    <div class="text-gray-500 text-xs" v-if="showNextModeLabel">
      Change to {{ nextMode }}
    </div>
    <button
      @click="toggleMode"
      @mouseenter="showNextModeLabel = true"
      @mouseleave="showNextModeLabel = false"
      class="hover:bg-gray-200 dark:hover:bg-gray-600 px-2 py-1 text-gray-500 rounded-md"
    >
      {{ nextModeIcon }}
    </button>
  </div>
</template>

<script setup>
const showNextModeLabel = ref(false);
const colorMode = useColorMode();

const modes = [
  "system", // 0
  "light", // 1
  "dark", // 2
]; // .length = 3

const nextModeIcons = {
  system: "🌓",
  light: "🌕",
  dark: "🌑",
};

const nextMode = computed(() => {
  const currentModeIndex = modes.indexOf(colorMode.preference);

  // (2 + 1) % 3 = 0 - resets the next mode
  return modes[(currentModeIndex + 1) % modes.length];
});

const nextModeIcon = computed(() => nextModeIcons[nextMode.value]);

const toggleMode = () => (colorMode.preference = nextMode.value);
</script>

<style></style>
