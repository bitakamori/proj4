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

        <button id="button2" @click="openModal">Click here!!</button>
        <div class="modal" v-if="isOpen">
      <div class="modal-content">
        <table class="table"> 
    <tr>
    <h1>Today's Advice:</h1>
    </tr>
    <tr v-for="conselho in adv" :key="conselho.advice"> 
    <td id ="tip">{{ conselho.advice }}</td>
    </tr>
    </table>
        <button  class="material-symbols-outlined" id="button1" @click="closeModal" >cancel</button>
        <Modal :isOpen="isModalOpen" @closeModal="closeModal" />

      </div>
    </div>



    </main>
</template>

<style scoped>

  @import url('https://fonts.googleapis.com/css2?family=Satisfy&display=swap');

  #tip {
    font-family: Satisfy, sans-serif;
  }

.material-symbols-outlined {
  font-variation-settings:
  'FILL' 0,
  'wght' 400,
  'GRAD' 0,
  'opsz' 48
}

#button1{
    background: transparent;
    border: none;
    color: red;
}

#button2{
    background: transparent;
    border: none;
    color: #8b008b;
    animation: pulsate 2s infinite;

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

.modal-content{
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