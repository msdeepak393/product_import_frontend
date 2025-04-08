<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-4">
        <h2 class="mb-4">Login</h2>
        <div v-if="errors.length" class="alert alert-danger">
          <ul class="mb-0">
            <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
          </ul>
        </div>
        <form @submit.prevent="login">
          <div class="mb-3">
            <label for="email" class="form-label">Email</label>
            <input v-model="form.email" type="email" class="form-control" id="email" required>
          </div>
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input v-model="form.password" type="password" class="form-control" id="password" required>
          </div>
          <button type="submit" class="btn btn-primary w-100">Login</button>
        </form>
        <p class="mt-3">
          Don't have an account? <router-link to="/register">Register here</router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from '../axios' 

export default {
  name: 'Login',
  data() {
    return {
      form: {
        email: '',
        password: '',
      },
      errors: [],
    }
  },
  methods: {

    async login() {
      try {
        const response = await axios.post('/login', {
          email: this.form.email,
          password: this.form.password,
          device_name: 'web_app'
        })

        localStorage.setItem('token', response.data.token)

        this.$router.push('/dashboard')
      } catch (error) {
        if (error.response && error.response.data.message) {
          this.errors = [error.response.data.message]
        } else if (error.response && error.response.data.errors) {
          this.errors = Object.values(error.response.data.errors).flat()
        } else {
          this.errors = ['Login failed. Please try again.']
        }
      }
    }
  }
}
</script>
