<template>
  <div id="modalA" class="modalWrapper modalA" v-if="isShow">
    <div class="modalContents">
      <h1>Moodl{{ name }}</h1>
      <p>Here are modal contents!</p>
    </div>
    <button v-on:click="closeModal" class="button" id="modalAButton">
      CLOSE
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useCount } from '~/composables/count'

interface Props {
  name: string
  isShow: boolean
}

export default defineComponent({
  name: 'Modal',
  props: {
    name: {
      type: String,
      default: '',
    },
    isShow: {
      type: Boolean,
      default: false,
    },
  },
  setup(props: Props) {
    console.log(props)

    const closeModal = (e) => {
      props.isShow = false
    }

    return {
      openModal,
      closeModal,
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
