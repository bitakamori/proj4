<script>
import Modal from "../components/Modal.vue";

export default {
  components: {
    Modal,
  },
  data() {
    return {
      adv: [],
      isOpen: false,
      title: "",
      text: "",
    };
  },
  methods: {
    getAdvice(url) {
      fetch(url)
        .then((res) => res.json())
        .then((data) => {
          this.adv = data;
        });
    },
    openModal(title, text) {
      this.isOpen = true;
      this.title = title;
      this.text = text;
    },
    closeModal() {
      this.isOpen = false;
      this.title = "";
      this.text = "";
    },
  },
  mounted() {
    this.getAdvice("https://api.adviceslip.com/advice");
  },
};
</script>

<template>
  <main>
    <div class="container">
      <svg viewBox="0 0 960 300">
        <symbol id="s-text">
          <text text-anchor="middle" x="50%" y="80%">Mom Dináh</text>
        </symbol>
        <g class="g-ants">
          <use xlink:href="#s-text" class="text-copy"></use>
          <use xlink:href="#s-text" class="text-copy"></use>
          <use xlink:href="#s-text" class="text-copy"></use>
          <use xlink:href="#s-text" class="text-copy"></use>
          <use xlink:href="#s-text" class="text-copy"></use>
        </g>
      </svg>
    </div>
    <button id="button2" @click="openModal">Click here!!</button>
    <div class="modal" v-if="isOpen">
      <div class="modal-content">
        <table class="table">
          <tr>
            <h1>Today's Advice:</h1>
          </tr>
          <tr v-for="conselho in adv" :key="conselho.advice">
            <td id="tip">{{ conselho.advice }}</td>
          </tr>
        </table>
        <button
          class="material-symbols-outlined"
          id="button1"
          @click="closeModal"
        >
          cancel
        </button>
        <Modal :isOpen="isModalOpen" @closeModal="closeModal" />
      </div>
    </div>
  </main>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Gloria+Hallelujah&display=swap");
@import url(https://fonts.googleapis.com/css?family=Montserrat);
svg {
  display: block;
  font: 10.5em "Montserrat";
  width: 600px;
  height: 300px;
  margin: 0 auto;
}

.text-copy {
  fill: none;
  stroke-dasharray: 6% 29%;
  stroke-width: 5px;
  stroke-dashoffset: 0%;
  animation: stroke-offset 5.5s infinite linear;
}

.text-copy:nth-child(1) {
  stroke: plum;
  animation-delay: -1;
}

.text-copy:nth-child(2) {
  stroke: rgb(180, 116, 180);
  animation-delay: -2s;
}

.text-copy:nth-child(4) {
  stroke: plum;
  animation-delay: -4s;
}

.text-copy:nth-child(5) {
  stroke: plum;
  animation-delay: -5s;
}

@keyframes stroke-offset {
  100% {
    stroke-dashoffset: -35%;
  }
}

main {
  width: 100vw;
  height: 100vh;
  overflow: hidden;

  background-image: url("/public/fundo.jpeg");
  background-repeat: no-repeat;
  background-size: 100%;
  z-index: 1%;
}

#tip {
  font-family: "Gloria Hallelujah", cursive;
}

.material-symbols-outlined {
  font-variation-settings:
  'FILL' 0,
  'wght' 400,
  'GRAD' 0,
  'opsz' 48
}

#button1 {
  background: transparent;
  border: none;
  color: red;
}

#button2 {
  background: transparent;
  border: none;
  color: #490f49;
  animation: pulsate 2s infinite;
  position: relative;
  margin: 17.5% 42%;

  font-size: 50px;

  width: 20rem;
}

@keyframes pulsate {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

.modal-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.table {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
