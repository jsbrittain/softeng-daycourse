<script setup lang="ts">
  const props = defineProps({
    class: {
      type: String,
    },
  })
</script>

<template>
  <div class="slidev-layout flex flex-col h-full">
    <div class="header">
      <slot />
    </div>

    <div
      class="flex-1 flex flex-col justify-center p-0"
      :class="class"
    >
      <slot name="centralise" />
    </div>
  </div>
</template>
