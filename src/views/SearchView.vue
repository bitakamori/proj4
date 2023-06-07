<script>
export default {
  data() {
    return {
      searchQuery: "",
      adviceList: [],
      advice: "",
      //temOutrosAdvices: false,
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
            this.advice = 'Everything is gonna be alright';
          }
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<template>
  <div>
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Give me a word and I will guide you"
    />
    <button @click="searchAdvice">Buscar</button>
    <p>{{
       advice
      }}</p> 
    <!-- <button :disabled="!temOutrosAdvices"></button> -->
  </div>
</template>


