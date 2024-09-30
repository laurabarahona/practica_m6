<template>
  <nav class="navbar">
    <div class="navbar-brand">
      <router-link to="/">Game Opinions</router-link>
    </div>

    <div class="navbar-links">
      <ul>
        <li>
          <router-link to="/">Home</router-link>
        </li>
      </ul>
    </div>

    <button class="navbar-toggler" @click="toggleMenu">
      &#9776;
    </button>

    <div class="navbar-collapse" v-show="isMenuOpen">
      <ul>
        <li>
          <router-link to="/">Home</router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false 
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen; 
    }
  }
};
</script>

<style scoped>
.navbar {
  background-color: #393939;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
}

.navbar-brand {
  color: white;
  font-size: 1.5rem;
}

.navbar-brand a {
  color: white;
  text-decoration: none;
}

.navbar-toggler {
  font-size: 1.5rem;
  background: none;
  color: white;
  border: none;
  cursor: pointer;
  display: none; 
}

.navbar-links {
  flex-grow: 1;
  display: flex;
  justify-content: flex-end;
}

.navbar-links ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.navbar-links li {
  margin-left: 20px;
}

.navbar-links a {
  color: white;
  text-decoration: none;
  font-size: 1rem;
  transition: color 0.3s ease;
}

.navbar-links a:hover {
  color: #ff9800; 
}

@media (max-width: 768px) {
  .navbar-toggler {
    display: block;
  }

  .navbar-links {
    display: none;
  }

  .navbar-collapse {
    background-color: #393939;
    display: block;
    position: absolute;
    top: 50px;
    right: 0;
    width: 100%;
    text-align: right;
  }

  .navbar-collapse ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .navbar-collapse li {
    margin: 10px 0;
  }

  .navbar-collapse a {
    padding: 10px;
    display: block;
    color: white;
    text-decoration: none;
  }
}
</style>
