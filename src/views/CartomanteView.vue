<script>
export default {
  data() {
    return {
      responseData: '',
      card: "string",
    };
  },
  methods: {
    async getCards() {
      try {
        const response = await fetch('https://tarot-api-3hv5.onrender.com/api/v1/cards/random?n=1');
        const data = await response.json();
        this.responseData = data;
        const { name, meaning_up, meaning_rev } = data; 
        this.card = {
          name: name,
          "Significado": meaning_up,
          "Descrição":meaning_rev,
        }
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<template>
  <div class="about">
    <button @click="getCards">Carta</button>
    <!-- <p> {{ responseData }}</p> -->
    <table>
    <tr v-for="(value, label) in responseData" :key="label">
      <th>{{ label }}</th>
      <td>{{ value }}</td>
    </tr>
  </table>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
