<script>
export default {
  data() {
    return {
      searchQuery: "",
      adviceList: [],
      advice: "",
      showTextEffect: false,
    };
  },
  methods: {
    searchAdvice() {
      const apiUrl = `https://api.adviceslip.com/advice/search/${this.searchQuery}`;

      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          if (data.slips && data.slips.length > 0) {
            this.advice = data.slips[0].advice;
          } else {
            this.advice = "Everything is gonna be alright";
          }
          this.showTextEffect = true;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<template>
  <main>
    <div>
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Give me a word and I will look into your future"
        class="custom-input"
      />
      <button @click="searchAdvice" class="material-icons">visibility</button>

      <div>
        <h1 class="text-effect" v-if="showTextEffect">{{ advice }}</h1>
      </div>
    </div>
  </main>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Satisfy&display=swap');

.text-effect {
  font-size: 48px;
  font-weight: bold;
  color: white;
  overflow: hidden;
  white-space: nowrap;
  animation: reveal-text 2s linear forwards;
  font-family: 'Satisfy', cursive;
}

.material-icons {
  font-family: 'Material Icons';
  font-size: 200px;
  font-weight: normal;
  font-style: normal;
  line-height: 1;
  letter-spacing: normal;
  text-transform: none;
  display: inline-block;
  white-space: nowrap;
  word-wrap: normal;
  direction: ltr;
  -webkit-font-feature-settings: 'liga';
  -webkit-font-smoothing: antialiased;
  background: transparent;
  border: none;
  color: white;
}

@keyframes reveal-text {
  0% {
    width: 0;
    opacity: 0;
    transform: translateX(0%);
  }
  100% {
    width: 100%;
    opacity: 1;
    transform: translateX(0);
  }
}

.custom-input {
  width: 400px; 
  padding: 10px; 
  border: white;
  border-style: dashed;
  background-color: #e8e6f3; 
  font-size: 16px; 
  color: #000; 
}

main {
  width: 100vw;
  height: 100vh;
  overflow: hidden;

  background-image: url("/public/bgsearch1.jpeg");
  background-repeat: no-repeat;
  background-size: 90%;
  z-index: 1%;
}


</style>

