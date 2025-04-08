<template>
  <div class="container mt-5">
    <h3 class="mb-4">📁 Upload CSV File</h3>

    <form @submit.prevent="uploadFile" enctype="multipart/form-data">
      <div class="mb-3">
        <label for="file" class="form-label">Choose CSV File</label>
        <input 
          type="file" 
          class="form-control" 
          id="file" 
          name="file" 
          @change="handleFileChange"
          accept=".csv"
          required
        >
      </div>

      <button type="submit" class="btn btn-primary" :disabled="isLoading">
        <span v-if="isLoading" class="spinner-border spinner-border-sm me-2" role="status" aria-hidden="true"></span>
        {{ isLoading ? 'Uploading...' : 'Upload' }}
      </button>
    </form>

    <div v-if="message" class="alert mt-4" :class="success ? 'alert-success' : 'alert-danger'">
      {{ message }}
    </div>
  </div>
</template>

<script>
import axios from '../axios'

export default {
  name: 'Upload',
  data() {
    return {
      file: null,
      message: '',
      success: false,
      isLoading: false
    }
  },
  methods: {
    handleFileChange(event) {
      this.file = event.target.files[0]
    },
    async uploadFile() {
      if (!this.file) return

      const formData = new FormData()
      formData.append('file', this.file)

      this.isLoading = true
      this.message = ''
      this.success = false

      try {
        const token = localStorage.getItem('token')
        const response = await axios.post('/import-product', formData, {
          headers: {
            Authorization: `Bearer ${token}`,
            'Content-Type': 'multipart/form-data',
          },
        })

        this.message = response.data.message || 'File uploaded successfully!'
        this.success = true
      } catch (error) {
        this.message = error.response?.data?.message || 'File upload failed.'
        this.success = false
      } finally {
        this.isLoading = false
      }
    },
  },
}
</script>

<style scoped>
h3 {
  font-weight: 600;
}
</style>
