<template>
  <div class="comments" v-if="game">
    <h1 class="comments-title">Opiniones sobre {{ game.name }}</h1>
    <div class="game-image">
      <img :src="game.background_image" alt="Imagen del juego" />
    </div>
    <p class="game-rating">⭐ {{ game.rating }}</p>
    <div class="comment-form-card">
      <form @submit.prevent="submitComment">
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Nombre</label>
          <input v-model="newComment.userName" type="text" class="form-control" id="exampleFormControlInput1" required />
        </div>
        <div class="mb-3">
          <label for="exampleFormControlTextarea1" class="form-label">Tu Opinión</label>
          <textarea v-model="newComment.userOpinion" class="form-control" id="exampleFormControlTextarea1" rows="3" required></textarea>
        </div>
        <button type="submit" class="btn btn-submit">
          {{ isEditing ? 'Actualizar' : 'Enviar' }}
        </button>
      </form>
    </div>
    <div class="comment-section" v-if="comments.length > 0">
      <h2>Otras opiniones</h2>
      <div v-for="(comment, index) in comments" :key="index" class="comment-card">
        <p class="comment-name">
          <strong>{{ comment.userName }}</strong> <span class="text-muted">dice:</span>
        </p>
        <p class="comment-content">{{ comment.userOpinion }}</p>
        <div class="comment-buttons">
          <button class="btn btn-edit" @click="editComment(index)">Editar</button>
          <button class="btn btn-delete" @click="deleteComment(index)">Eliminar</button>
        </div>
      </div>
    </div>
    <div v-else class="alert no-comments" role="alert">
      No hay opiniones para mostrar
    </div>
  </div>
  <div v-else class="waiting">
    <p>Cargando...</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      game: null,
      newComment: {
        userName: '',
        userOpinion: ''
      },
      isEditing: false,
      editingIndex: null,
      comments: []
    };
  },
  async created() {
    const gameName = this.$route.params.gameName; 
    let games = this.$route.params.games; 

    // OJO ESTO "PARCHA" EL PROBLEMA DE PERDER EL JUEGO AL REFRESCAR - TENGO QUE APRENDER A MANEJAR VUEX
    if (!games) {
      try {
        const response = await fetch(`https://api.rawg.io/api/games?key=f9bc18700f2c4b1b946c99bbd19547ef&search=${gameName}`);
        const data = await response.json();
        games = data.results; 
      } catch (error) {
        console.error("Error al obtener el juego desde la API:", error);
      }
    }
    this.game = games ? games.find(game => game.name.toLowerCase() === gameName.toLowerCase()) : null;
    if (!this.game) {
      this.$router.replace({ name: 'NotFoundView' });
    }
  },
  methods: {
    submitComment() {
      if (this.isEditing) {
        this.comments[this.editingIndex] = { ...this.newComment };
        this.isEditing = false;
        this.editingIndex = null;
      } else {
        this.comments.push({ ...this.newComment });
      }
      this.newComment.userName = '';
      this.newComment.userOpinion = '';
    },
    editComment(index) {
      this.isEditing = true;
      this.editingIndex = index;
      this.newComment = { ...this.comments[index] };
    },
    deleteComment(index) {
      this.comments.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.comments {
  max-width: 600px;
  margin: 20px auto;
  text-align: center;
  padding: 20px;
}

.comments-title {
  color: white;
  font-weight: bold;
  margin-bottom: 25px;
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}

.game-image img {
  width: 100%;
  max-height: 300px;
  object-fit: cover;
  margin-bottom: 20px;
}

.game-rating {
  font-size: 1.8em; 
  margin-bottom: 50px;
  color: #555;
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}

.form-label {
  color: white; 
  font-weight: bold;
}

.form-control {
  background-color: #e0e0e0; 
  color: #000; 
}

.btn-submit, .btn-edit, .btn-delete {
  background-color: #495c5a !important; 
  color: white !important;
  border: none !important;
  padding: 10px !important;
  margin-top: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease !important;
}

.btn-submit:hover, .btn-edit:hover, .btn-delete:hover {
  background-color: #121212 !important; 
}

.btn-submit:active, .btn-edit:active, .btn-delete:active {
  background-color: #4a4a4a !important; 
}

.comment-section {
  margin-top: 30px;
}

.comment-card {
  background-color: #c8cacc;
  padding: 15px;
  margin-bottom: 15px;
  border: 1px solid #ddd;
  border-radius: 10px;
  text-align: left;
}

.comment-name {
  font-size: 1em;
  margin-bottom: 5px;
}

.comment-content {
  background-color: #c8cacc;
  padding: 10px;
  border-radius: 5px;
}

.comment-buttons {
  display: flex;
  gap: 10px;
}

.no-comments {
  background-color: #7a7a7a;
  color: white;
  font-weight: bold;
  text-align: center;
  margin-top: 30px;
}

h2{
  color: white;
  font-weight: bold;
  margin-top: 80px;
  margin-bottom: 35px;
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}

.waiting{
  color: white;
  font-size: 30px;
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  margin-top: 20px;
}
</style>
