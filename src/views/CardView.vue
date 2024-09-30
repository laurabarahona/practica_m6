<template>
  <div class="game-card">
    <div class="game-card-image">
      <img :src="game.background_image" alt="Imagen del juego" class="game-img">
    </div>
    <div class="game-card-details">
      <h3>{{ game.name }}</h3>
      <p><strong><i class="fas fa-star"></i> Rating:</strong> {{ game.rating }}</p>
      <p><strong><i class="fas fa-calendar-alt"></i> Lanzamiento:</strong> {{ game.released }}</p>
      <p><strong>Última actualización:</strong> {{ game.updated }}</p>
    </div>
    <div class="game-card-actions">
      <button class="opinion-btn" @click="goToComments">
        <i class="fas fa-pencil-alt"></i> Opinar
      </button>
      <button class="like-btn" @click="toggleLike">
        <span :style="{ color: isLiked ? 'red' : 'inherit' }">&hearts;</span>
        {{ isLiked ? 'Liked' : 'Like' }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    game: Object
  },
  data() {
    return {
      isLiked: false 
    };
  },
  methods: {
    goToComments() {
      this.$router.push({
        name: 'CommentsView',
        params: {
          gameName: this.game.name,
          gameImage: this.game.background_image,
          gameRating: this.game.rating
        }
      });
    },
    toggleLike() {
      this.isLiked = !this.isLiked;
    }
  }
};
</script>

<style scoped>

.game-card {
  background-color: #1f1e1e;
  border-radius: 10px;
  color: #dedddd;
  padding: 20px;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: transform 0.5s ease; 
}

.game-card:hover {
  transform: scale(1.05);
}

.game-card-image img {
  width: 100%;
  height: 250px;
  object-fit: cover;
}

.game-card-details h3 {
  margin-top: 10px;
}

.game-card-details p {
  margin: 5px 0;
}

.game-card-actions {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.opinion-btn, .like-btn {
  width: 50%;
  padding: 10px 0;
  border: 1px solid #ccc;
  background-color: #afacac;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: background-color 0.2s ease;
}

.opinion-btn {
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

.like-btn {
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

.opinion-btn:hover {
  background-color: #6c757d; 
}

.opinion-btn:active {
  background-color: #5a6268; 
}

.like-btn:hover {
  background-color: #6c757d; 
}

.like-btn:active {
  background-color: #5a6268; 
}

</style>
