<template>
  <div>
    <CalendarioComp />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CalendarioComp from './components/CalendarioComp.vue'

export default defineComponent({
  name: 'App',
  components: { CalendarioComp }
});
</script>

<style>
</style>
