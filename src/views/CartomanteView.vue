<script>

export default {
  data() {
    return {
      // Inicializando lista de cards que vc vai utilizar
      cards: [],
    };
  },
  methods: {
    async getCards() {
      try {
        // dando fetch na api, que é, buscando um dado de um endpoint
        // Nesse caso, seguindo a documentação da api estamos pegando 3 random cards
        let response = await fetch(
          "https://tarot-api-3hv5.onrender.com/api/v1/cards/random?n=3"
        );
        // Colocar a resposta no formation JSON
        let data = await response.json();
        // sempre que tentar pegar algo de uma api de console.log na response.json, que nesse caso atribuimos a variavel data
        console.log(data);
        // Como demos console log, sabemos que nessa api a lista de cards que qremos está em data.cards
        let responseData = data.cards;
        // Dando console log pra ter certeza
        console.log(data.cards);
        // Como response.data agr é data.cards, ou seja, uma lista de cards, usamos o forEach para iterar sobre cada card
        // Para cada card em responseData(data.cards), demos push, ou seja, adicionamos a card que está sendo iterada na variavel cards
        // A variável cards está sendo definida de forma global, então poderemos acessar ela dps no html pra iterar sobre ela e renderizar as propriedades dela

        this.cards = responseData;
        responseData.forEach((card) => {
          this.cards.push(card);
        });
        // Deixei um for aqui pra vc comparar com o forEach
        // for (let i =0; i < this.cards.length; i++) ... this.cards[i]
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
<template>
  <div>
    <Card :name="card.name"  :meaning_up="card.meaning_up" :meaning_rev="card.meaning_rev" v-for="card in cards" />
  </div>

  <div class="about">
    <button @click="getCards">Carta</button>
    <!-- <p> {{ responseData }}</p> -->

    <table>
      <tr>
        <th>Name</th>
        <th>Description up</th>
        <th>Description rev</th>
      </tr>
      <!-- Essa é a estrutura de for do vue para iterar para cada dado de uma lista -->
      <tr v-for="card in cards" :key="card.name">
        <!-- a key é obrigatória qnd iteramos sobre uma lista, ela é apenas o identificador do item que vc ta iterando -->
        <!-- Como card vem da resposta da api podemos acessar as propriedades dela, so precisamos saber qm são essas propriedades -->
        <!-- Fica facil saber certingo quais sao as propriedades uma vez que a gente deu console log no cards -->
        <td>{{ name }}</td>
        <td>{{ meaning_up }}</td>
        <td>{{ meaning_rev }}</td>
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
