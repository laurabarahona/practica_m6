<template>
  <div class="container-fluid not-found">
    <div class="content">
      <h1>404</h1>
      <h1>UPS!</h1>
      <p>La página que estás buscando no existe</p>
      <router-link to="/" class="btn btn-home">Volver al inicio</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "NotFoundView"
};
</script>

<style scoped>
.not-found {
  min-height: 100vh; 
  background-image: linear-gradient(to right, rgba(0,0,0,1) 0%, rgba(0,0,0,0.7) 20%, rgba(0,0,0,0) 50%, rgba(0,0,0,0.7) 80%, rgba(0,0,0,1) 100%), url('@/assets/straycat.jpg'); 
  background-size: cover; 
  background-position: center center; 
  background-repeat: no-repeat; 
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: white;
  font-family: 'Arial', sans-serif;
}

.content {
  position: relative;
  z-index: 2; 
}

h1 {
  font-size: 6rem; 
  margin-bottom: 20px;
  font-weight: bold;
}

p {
  font-size: 1.5rem;
  margin-bottom: 30px;
}

.btn-home {
  background-color: #6a7676 !important;
  color: white !important;
  border: none !important;
  padding: 10px 20px !important;
  cursor: pointer;
  text-decoration: none;
  font-size: 1.2rem;
  transition: background-color 0.3s ease !important;
}

.btn-home:active {
  background-color: #4a4a4a !important;
}

.btn-home:hover {
  background-color: #585c5b !important;
}
</style>
