<script>
  export default {
    data() {
      return {
        isOpen: false,
        title: '',
        text: ''
      };
    },
    methods: {
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
    }
  };
  </script>
  
  <template>
    <div class="modal" v-if="isOpen">
      <div class="modal-content">
        <h2>{{ title }}</h2>
        <p>{{ text }}</p>
      </div>
    </div>
  </template>
  
  <style>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal-content {
    background-color: black;
    color: rgb(98, 10, 180);
    font-size: 50px;
    opacity: 80%;
    padding: 50px;
    border-radius: 8px;
  }
  
  h2 {
    margin-top: 0;
  }
  
  button {
    margin-top: 10px;
  }
  </style>