<template>
  <div class="container mt-5">
    <h3 class="mb-4">📦 Uploaded Products</h3>

    <div v-if="loading">Loading products...</div>
    <div v-else-if="products.length === 0">No products found.</div>

    <table v-else class="table table-bordered table-striped">
      <thead>
        <tr>
          <th>#</th>
          <th>Product Name</th>
          <th>Price</th>
          <th>SKU</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(product, index) in products" :key="product.id">
          <td>{{ index + 1 }}</td>
          <td>{{ product.name }}</td>
          <td>₹ {{ product.price }}</td>
          <td>{{ product.sku }}</td>
          <td>{{ product.description }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from '../axios'

export default {
  name: 'Products',
  data() {
    return {
      products: [],
      loading: true,
    }
  },
  async created() {
    try {
      const token = localStorage.getItem('token')
      const response = await axios.get('/products', {
        headers: {
          Authorization: `Bearer ${token}`,
        },
      })

      this.products = response.data.data
    } catch (error) {
      console.error('Error fetching products:', error)
    } finally {
      this.loading = false
    }
  },
}
</script>

<style scoped>
h3 {
  font-weight: 600;
}
</style>
