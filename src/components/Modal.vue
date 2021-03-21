<template>
  <div>
    <div>
      <input type="checkbox" value="1" v-model="state.modalOpenChecks">
      <label for="1">1</label>
      <input type="checkbox" value="2" v-model="state.modalOpenChecks">
      <label for="2">2</label>
      <input type="checkbox" value="3" v-model="state.modalOpenChecks">
      <label for="3">3</label>
    </div>
    <button v-on:click="openModal" class="button">OPEN</button>
    <div class="modalArea" v-if="state.showArea">
      <div class="modalBg" v-on:click="closeModalAll" ></div>
      <div id="modalA" class="modalWrapper modalA" v-if="state.showContent1">
        <div class="modalContents">
          <h1>ModalA</h1>
          <p>Here are modal contents!</p>
        </div>
         <button v-on:click="closeModal" class="button" id="modalAButton">CLOSE</button>
      </div>

      <div id="modalB" class="modalWrapper modalB" v-if="state.showContent2">
        <div class="modalContents">
          <h1>ModalB</h1>
          <p>Here are modal contents!</p>
        </div>
         <button v-on:click="closeModal" class="button" id="modalBButton">CLOSE</button>
      </div>

      <div id="modalC" class="modalWrapper modalC" v-if="state.showContent3">
        <div class="modalContents">
          <h1>ModalC</h1>
          <p>Here are modal contents!</p>
        </div>
         <button v-on:click="closeModal" class="button" id="modalCButton">CLOSE</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive} from 'vue'
import { useCount } from '~/composables/count'

interface State {
  showArea: boolean;
  showContent1: boolean;
  showContent2: boolean;
  showContent3: boolean;
  modalOpenChecks: string[];
}

export default defineComponent({
  name: 'Modal',
  setup () {
    const state = reactive<State>({
      showArea: false,
      showContent1: false,
      showContent2: false,
      showContent3: false,
      modalOpenChecks: []
    })

    const openModal = () =>{
      if (state.modalOpenChecks.includes("1")) {
        state.showContent1 = true
      }
      if (state.modalOpenChecks.includes("2")) {
        state.showContent2 = true
      }
      if (state.modalOpenChecks.includes("3")) {
        state.showContent3 = true
      }
      if (state.modalOpenChecks.length > 0) {
        state.showArea = true
      }
    }

    const closeModal = (e) =>{
      if (e.target.id === 'modalAButton') state.showContent1 = false
      if (e.target.id === 'modalBButton') state.showContent2 = false
      if (e.target.id === 'modalCButton') state.showContent3 = false
      if(!state.showContent1 && !state.showContent2 && !state.showContent3) state.showArea = false
    }

    const closeModalAll = () =>{
      state.showContent1 = false
      state.showContent2 = false
      state.showContent3 = false
      state.showArea = false
    }

    return {
      state,
      openModal,
      closeModal,
      closeModalAll
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

.modalA {
  z-index:1
}
.modalB {
  z-index:2
}
.modalC {
  z-index:3
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
