<script lang="ts">
import InputGroup from './components/Input-group.vue'
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      perspective: 100,
      rotateX: 0,
      rotateY: 0,
      rotateZ: 0
    }
  },
  methods: {
    async copyStyle() {
      await navigator.clipboard.writeText(JSON.stringify(this.box))
      alert('Copied to clipboard!')
    }
  },
  computed: {
    box() {
      return {
        transform: `perspective(${this.perspective}px) rotateX(${this.rotateX}deg) rotateY(${this.rotateY}deg) rotateZ(${this.rotateZ}deg)`
      }
    }
  },
  components: {
    InputGroup
  }
})
</script>

<template>
  <h1>CSS3 Perspective Playground</h1>

  <main>
    <div class="inputs">
      <InputGroup label="perspective" v-model="perspective" />
      <InputGroup label="rotateX" v-model="rotateX" />
      <InputGroup label="rotateY" v-model="rotateY" />
      <InputGroup label="rotateZ" v-model="rotateZ" />
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
