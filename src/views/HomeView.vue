<script>
import Modal from '../components/Modal.vue'

export default {
    components: {
    Modal
    },
    data() {
        return {
            adv: [],
            isOpen: false,
            title: '',
            text: ''
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
        this.title = '';
        this.text = '';
      }
    },
    mounted(){
        this.getAdvice("https://api.adviceslip.com/advice");
    }
}
</script>

<template>
    <main>
        <div class="container">
  <svg viewBox="0 0 960 300">
    <symbol id="s-text">
      <text text-anchor="middle" x="50%" y="80%">Mom Dináh</text>
    </symbol>

    <g class = "g-ants">
      <use xlink:href="#s-text" class="text-copy"></use>
      <use xlink:href="#s-text" class="text-copy"></use>
      <use xlink:href="#s-text" class="text-copy"></use>
      <use xlink:href="#s-text" class="text-copy"></use>
      <use xlink:href="#s-text" class="text-copy"></use>
    </g>
  </svg>
</div>
        <button id="button2" @click="openModal">Abrir Modal</button>
        <div class="modal" v-if="isOpen">
      <div class="modal-content">
        <table>
    <tr>
    <th>Advice</th>
    </tr>
    <tr v-for="conselho in adv" :key="conselho.advice">
    <td>{{ conselho.advice }}</td>
    </tr>
    </table>
        <button @click="closeModal">Fechar</button>
        <Modal :isOpen="isModalOpen" @closeModal="closeModal" />

      </div>
    </div>
    </main>
</template>

<style scoped>
@import url(https://fonts.googleapis.com/css?family=Montserrat);


svg {
    display: block;
    font: 10.5em 'Montserrat';
    width: 600px;
    height: 300px;
    margin: 0 auto;
}

.text-copy {
    fill: none;
    /* stroke: rgb(255, 255, 255); */
    stroke-dasharray: 6% 29%;
    stroke-width: 5px;
    stroke-dashoffset: 0%;
    animation: stroke-offset 5.5s infinite linear;
}

.text-copy:nth-child(1){
	/* stroke: #b68393; */
    stroke: plum;
	animation-delay: -1;
}

.text-copy:nth-child(2){
	/* stroke: #793954; */
    stroke: rgb(180, 116, 180);
	animation-delay: -2s;
}

/* .text-copy:nth-child(3){
	stroke: #7b5b7e;
    stroke: plum;
	animation-delay: -3s;
} */

.text-copy:nth-child(4){
	/* stroke: #854d88; */
    stroke: plum;
	animation-delay: -4s;
}

.text-copy:nth-child(5){
	/* stroke: #bb6284;  */
    stroke: plum;
	animation-delay: -5s;
}

@keyframes stroke-offset{
	100% {stroke-dashoffset: -35%;}
}

main {
width: 100vw;
height: 100vh;
overflow: hidden;

background-image: url("https://i.pinimg.com/564x/40/43/3d/40433d9463f38b56d49c70023ef4bac9.jpg");
  background-repeat: no-repeat;
  background-size: 30%;
  background-position: center;
  z-index: 1%;
}

#button2{
    position: relative;
    margin: 23rem 55rem;
}

</style>