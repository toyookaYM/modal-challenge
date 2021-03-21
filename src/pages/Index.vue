<template>
  <Modal msg="Hello Vue 3 + TypeScript + Vite" />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Modal from '~/components/Modal.vue'

export default defineComponent({
  name: 'App',
  components: {
    Modal,
  },
})
</script>

<style></style>
