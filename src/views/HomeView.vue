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

        <button @click="openModal">Abrir Modal</button>
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