<script>
import Loader from "../components/Loader.vue";

export default {
  data() {
    return {
      // Inicializando lista de cards que vc vai utilizar
      cards: [],
      loading: false,
    };
  },
  components: {
    Loader,
  },
  methods: {
    async getCards() {
      try {
        this.loading = true;
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
        // Deixei um for aqui pra vc comparar com o forEach
        // for (let i =0; i < this.cards.length; i++) ... this.cards[i]
      } catch (error) {
        console.error(error);
      }

      this.loading = false;
    },
  },
};
</script>
<template>
  <main>
    <!-- <div>
    <Card :name="card.name"  :meaning_up="card.meaning_up" :meaning_rev="card.meaning_rev" v-for="card in cards" />
  </div> -->
    <div class="about">
      <!-- <p> {{ responseData }}</p> -->
      <div id="loading" v-if="loading">
        <loader></loader>
      </div>
      <table class="table-content">
        <!-- Essa é a estrutura de for do vue para iterar para cada dado de uma lista -->
        <tr v-for="card in cards" :key="card.name" class="tarot">
          <!-- a key é obrigatória qnd iteramos sobre uma lista, ela é apenas o identificador do item que vc ta iterando -->
          <!-- Como card vem da resposta da api podemos acessar as propriedades dela, so precisamos saber qm são essas propriedades -->
          <!-- Fica facil saber certingo quais sao as propriedades uma vez que a gente deu console log no cards -->
          <div class="card-grid">
            <td class="card-name">{{ card.name }}</td>
            <td class="card-up"> Atributes:<br/> {{ card.meaning_rev }}</td>
            <td class="card-rev">Description:<br/> {{ card.meaning_up }}</td>
          </div>
        </tr>
      </table>
      <button class="image-button" @click="getCards"> Pick your card </button>
    </div>
  </main>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Dosis&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Merriweather:wght@300&display=swap');
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    
  }
}

#loading {
  position: fixed;
  top: 45%;
}

.table-content {
  display: flex;
  position: fixed;
  top: 13%;
  right: 17.1%;
}

.image-button {
   /* width: 250px; */
  /* height: 450px; */
  /* background-image: url(https://thumbs.dreamstime.com/b/magia-tarot-card-noturno-celestial-com-estrelas-quadro-para-previs%C3%B5es-astrologicas-de-bruxaria-nasce-uma-nova-estrela-vetor-211417547.jpg); */
  /* background-size: cover;
  background-position: center; */
  /* margin: 0; */
  font-size: 55px;
  font-family: 'Merriweather', serif;
  color: #DFC897;
  background: transparent;
  border: none;
  cursor: grab;
  position: fixed;
  bottom: 13%;
}

.card-name {
  height: 40px;
  width: 90%;
  margin-top: 8px;
  /* margin-bottom: 10px; */
  border: 1px solid white;
  background-color: #DFC897;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5%;

  font-family: "Bebas Neue", cursive;
  font-size: 20px;
  letter-spacing: 0px;
  word-spacing: 0px;
  color: #2C2B2E;
  font-weight: bold;
  text-decoration: none;
  font-style: italic;
  font-variant: normal;
  text-transform: uppercase;
  text-shadow: 2px 2px 4px white;
}

.card-up {
  min-height: 150px;
  width: 90%;
  /* margin-bottom: 5px; */
  border: 1px solid white;
  background-color: #DFC897;;
  border-radius: 8%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-size: 20px;
  font-family: "Dosis", sans-serif;
  color: #2C2B2E;
  padding: 20px;
}

/* .title {
  font-weight: bold;
} */

.card-rev {
  min-height: 280px;
  width: 90%;
  margin-bottom: 8px;
  border: solid 1px white;
  background-color: #DFC897;
  border-radius: 10%;
  font-size: 18px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 20px;
  font-family: "Dosis", sans-serif;
  color: #2C2B2E;
}

.card-grid {
  width: 380px;
  height: 580px;
  border: 10px solid #DFC897;;
  border-radius: 8%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  text-align: center;
  align-items: center;
  background-color: whitesmoke;
  padding: 5px;
  margin-left: 2.5rem;
}

.about {
  display: flex;
  flex-wrap: wrap;
}

.tarot {
  animation: deslizar 1s;
}

main {
  width: 100vw;
  height: 100vh;

  /* background-image: url(https://cdn.steamstatic.com/steamcommunity/public/images/items/447120/f173d53b9c696240fba8c45b6ec735f7bc1ce01a.jpg); */
  background-image: url("/public/celestial1.jpeg");
  background-repeat: no-repeat;
  background-size: 100%;
  background-position: center;
  z-index: 1%;
}

@keyframes deslizar {
  0% {
    top: -100px;
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    top: 0;
    opacity: 1;
  }
}
</style>
