<template>
  <div class="home">
    <section>
      <h1>NUESTROS JUEGOS</h1>
      <div class="game-grid">
        <CardView 
          v-for="game in games.slice(0, 15)" 
          :key="game.id" 
          :game="game" 
        />
      </div>
    </section>
  </div>
</template>

<script>
import CardView from './CardView.vue';

export default {
  name: 'HomeView',
  components: {
    CardView 
  },
  data() {
    return {
      games: []
    };
  },
  methods: {
    async fetchGames() {
      try {
        const response = await fetch("https://api.rawg.io/api/games?key=f9bc18700f2c4b1b946c99bbd19547ef&dates=2019-09-01,2019-09-30&platforms=18,1,7");
        if (!response.ok) {
          throw new Error("Error al obtener los juegos");
        }
        const data = await response.json();
        this.games = data.results;
      } catch (error) {
        console.error("Error al obtener los juegos:", error);
      }
    }
  },
  async created() {
    await this.fetchGames();
  }
};
</script>

<style scoped>
.game-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); 
  gap: 20px;
  margin-bottom: 50px; 
}

@media (max-width: 990px) { 
  .game-grid {
    grid-template-columns: repeat(2, 1fr); 
  }
}

@media (max-width: 670px) { 
  .game-grid {
    grid-template-columns: 1fr; 
  }
}

h1 {
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  font-size: 3.3rem;
  margin-top: 30px;
  margin-bottom: 25px;
  color: white;
}
</style>
