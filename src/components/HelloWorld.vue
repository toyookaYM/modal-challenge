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
      <div class="modalBg" v-on:click="closeModal" ></div>
      <div class="modalWrapper modal1" v-if="state.showContent1">
        <div class="modalContents">
          <h1>ModalA</h1>
          <p>Here are modal contents!</p>
        </div>
         <button v-on:click="closeModal1" class="button">CLOSE</button>
      </div>

      <div class="modalWrapper modal2"  v-if="state.showContent2">
        <div class="modalContents">
          <h1>ModalB</h1>
          <p>Here are modal contents!</p>
        </div>
         <button v-on:click="closeModal2" class="button">CLOSE</button>
      </div>

      <div class="modalWrapper modal3" v-if="state.showContent3">
        <div class="modalContents">
          <h1>ModalC</h1>
          <p>Here are modal contents!</p>
        </div>
         <button v-on:click="closeModal3" class="button">CLOSE</button>
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
  name: 'HelloWorld',
  setup () {
    const state = reactive<State>({
      showArea: false,
      showContent1: false,
      showContent2: false,
      showContent3: false,
      modalOpenChecks: []
    })

    const openModal = () =>{
      console.log(state.modalOpenChecks)
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

    const closeModal1 = () =>{
      state.showContent1 = false
      if(!state.showContent1 && !state.showContent2 && !state.showContent3) {
        state.showArea = false
      }
    }

    const closeModal2 = () =>{
      state.showContent2 = false
      if(!state.showContent1 && !state.showContent2 && !state.showContent3) {
        state.showArea = false
      }
    }

    const closeModal3 = () =>{
      state.showContent3 = false
      if(!state.showContent1 && !state.showContent2 && !state.showContent3) {
        state.showArea = false
      }
    }

    const closeModal = () =>{
      state.showContent1 = false
      state.showContent2 = false
      state.showContent3 = false
      state.showArea = false
    }

    return {
      state,
      openModal,
      closeModal,
      closeModal1,
      closeModal2,
      closeModal3
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
.modalWrapper2 {
  position: absolute;
  top: 45%;
  left: 45%;
  transform:translate(-50%,-50%);
  width: 70%;
  max-width: 500px;
  padding: 10px 30px;
  background-color: #fff;
}
.modalWrapper3 {
  position: absolute;
  top: 55%;
  left: 55%;
  transform:translate(-50%,-50%);
  width: 70%;
  max-width: 500px;
  padding: 10px 30px;
  background-color: #fff;
}
.modal1 {
  z-index:1
}
.modal2 {
  z-index:2
}
.modal3 {
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
