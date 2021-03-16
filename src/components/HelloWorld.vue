<template>
  <div>
    <button v-on:click="openModal" class="button">OPEN</button>
    <div class="modalArea" v-if="state.showContent">
      <div class="modalBg" v-on:click="closeModal" ></div>
      <div class="modalWrapper">
        <div class="modalContents">
          <h1>Here are modal title!</h1>
          <p>Here are modal contents!</p>
        </div>
         <button v-on:click="closeModal" class="button">CLOSE</button>
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

<style>
/* モーダルCSS */
.modalArea {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.modalBg {
  width: 100%;
  height: 100%;
  background-color: rgba(30,30,30,0.9);
}

.modalWrapper {
  position: absolute;
  top: 50%;
  left: 50%;
  transform:translate(-50%,-50%);
  width: 70%;
  max-width: 500px;
  padding: 10px 30px;
  background-color: #fff;
}

/*ボタンスタイル */
.button {
	padding: 10px;
  background-color: #fff;
  border: 1px solid #282828;
  border-radius: 2px;
  cursor: pointer;
}
</style>
