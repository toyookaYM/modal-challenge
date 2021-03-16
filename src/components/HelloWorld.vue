<template>
    <div id="app">

    <button v-on:click="openModal">Click</button>

    <div id="overlay">
        <div id="content" v-show="state.showContent">
          <p>モーダル</p>
          <button v-on:click="closeModal">Close</button>
        </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive} from 'vue'
import { useCount } from '~/composables/count'

interface State {
  showContent: boolean;
}

export default defineComponent({
  name: 'HelloWorld',
  setup () {
    const state = reactive<State>({
      showContent: false
    })

    const openModal = () =>{
      state.showContent = true
    }

    const closeModal = () =>{
      state.showContent = false
    }

    return {
      state,
      openModal,
      closeModal
    }
  }
})
</script>

<style scoped>


</style>
