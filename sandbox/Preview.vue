<script setup lang="ts">
import DropDown from '../src/components/DropDown.vue'
</script>

<template>
  <main class="container col align justify center">
    <DropDown top label="Label" theme="light" width="100px">
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
      <span class="list-item">Kurwa</span>
    </DropDown>
  </main>
</template>

<style scoped lang="scss">
main {
  font-family: system-ui;

  position: relative;

  display: flex;
  flex-direction: column;

  justify-content: center;
  align-items: center;

  width: 100vw;
  height: 100svh;
}
</style>
