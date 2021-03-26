<template>
  <div>
    <div>
      <input type="checkbox" value="1" v-model="state.ModalItems[0].isShow" />
      <label for="1">1</label>
      <input type="checkbox" value="2" v-model="state.ModalItems[1].isShow" />
      <label for="2">2</label>
      <input type="checkbox" value="3" v-model="state.ModalItems[2].isShow" />
      <label for="3">3</label>
    </div>
    <button v-on:click="openModal" class="button">OPEN</button>
    <div class="modalArea" v-if="state.showArea">
      <div class="modalBg" v-on:click="closeModalAll" />
      <Modal
        v-for="modal in state.ModalItems"
        :key="modal.id"
        :name="modal.name"
        :isShow="modal.isShow"
      >
      </Modal>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue'
import Modal from '~/components/Modal.vue'

interface Modal {
  readonly id: number
  readonly name: string
  isShow: boolean
}
interface State {
  showArea: boolean
  ModalItems: Modal[]
}

export default defineComponent({
  name: 'App',
  components: {
    Modal,
  },
  setup() {
    const state = reactive<State>({
      showArea: false,
      ModalItems: [
        {
          id: 1,
          name: 'A',
          isShow: false,
        },
        {
          id: 2,
          name: 'B',
          isShow: false,
        },
        {
          id: 3,
          name: 'C',
          isShow: false,
        },
      ],
    })

    const openModal = () => {
      console.log(state.ModalItems)
      // if (state.modalOpenChecks.includes('1')) {
      //   state.showContent1 = true
      // }
      // if (state.modalOpenChecks.includes('2')) {
      //   state.showContent2 = true
      // }
      // if (state.modalOpenChecks.includes('3')) {
      //   state.showContent3 = true
      // }
      if (state.ModalItems.length > 0) {
        state.showArea = true
      }
    }

    const closeModalAll = () => {
      state.ModalItems.map = false
      state.showContent2 = false
      state.showContent3 = false
      state.showArea = false
    }

    return {
      state,
      openModal,
      closeModal,
      closeModalAll,
    }
  },
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
  background-color: rgba(30, 30, 30, 0.9);
}

.modalWrapper {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 70%;
  max-width: 500px;
  padding: 10px 30px;
  background-color: #fff;
}

.modalA {
  z-index: 1;
}
.modalB {
  z-index: 2;
}
.modalC {
  z-index: 3;
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
