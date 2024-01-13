<script setup lang="ts">
import { computed, ref } from 'vue'

const perspective = ref(100)
const rotateX = ref(0)
const rotateY = ref(0)
const rotateZ = ref(0)
const box = computed(() => {
  return {
    transform: `perspective(${perspective.value}px) rotateX(${rotateX.value}deg) rotateY(${rotateY.value}deg) rotateZ(${rotateZ.value}deg)`
  }
})

const copyStyle = async () => {
  await navigator.clipboard.writeText(JSON.stringify(box.value))
  alert('Copied to clipboard!')
}
</script>

<template>
  <h1>CSS3 Perspective Playground</h1>

  <main>
    <div class="inputs">
      <div class="input">
        <span>perspective: {{ perspective }}px</span>
        <input type="range" v-model="perspective" min="0" max="999" />
      </div>
      <div class="input">
        <span>rotateX: {{ rotateX }}px</span>
        <input type="range" v-model="rotateX" min="-180" max="180" />
      </div>
      <div class="input">
        <span>rotateY: {{ rotateY }}px</span>
        <input type="range" v-model="rotateY" min="-180" max="180" />
      </div>
      <div class="input">
        <span>rotateZ: {{ rotateZ }}px</span>
        <input type="range" v-model="rotateZ" min="-180" max="180" />
      </div>
    </div>
    <div class="outside">
      <div class="box" :style="box"></div>
    </div>
  </main>
  <span class="copy" @click.prevent="copyStyle">
    {{ box }}
  </span>
</template>

<style scoped>
.copy {
  cursor: pointer;
}

main {
  display: flex;
  gap: 6rem;

  .inputs {
    .input {
      display: flex;
      flex-direction: column;
    }
  }

  .outside {
    display: grid;
    place-items: center;
    outline: 2px solid var(--color-heading);
    width: 200px;
    height: 200px;

    .box {
      background: var(--color-text);
      width: 100px;
      aspect-ratio: 1/1;
    }
  }
}
</style>
