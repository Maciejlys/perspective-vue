<script setup lang="ts">
defineProps({
  label: String
})
const proxyValue = defineModel()
</script>

<template>
  <div class="input">
    <span>{{ label }}: {{ proxyValue }}px</span>
    <input type="range" v-model="proxyValue" min="0" max="999" />
  </div>
</template>

<style scoped></style>
