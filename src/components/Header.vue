<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light mb-4">
    <div class="container-fluid">
      <router-link class="navbar-brand" to="/dashboard">My App</router-link>
      <div class="collapse navbar-collapse">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/upload">Upload Product</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/products">View Products</router-link>
          </li>
        </ul>
        <button class="btn btn-outline-danger" @click="logout">Logout</button>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from '../axios'

export default {
  name: 'Header',
  methods: {
    async logout() {
      try {
        const token = localStorage.getItem('token');

        await axios.post('/logout', {}, {
          headers: {
            Authorization: `Bearer ${token}`
          }
        });

        localStorage.removeItem('token');
        this.$router.push('/login');
      } catch (error) {
        console.error('Logout failed:', error);
        alert('Logout failed');
      }
    }
  }
}
</script>
