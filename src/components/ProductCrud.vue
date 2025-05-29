<template>
  <div class="container mt-4">
    <h2>Product CRUD</h2>

    <form @submit.prevent="saveProduct">
      <div class="mb-3">
        <input v-model="form.name" type="text" placeholder="Product name" class="form-control" required />
      </div>
      <button type="submit" class="btn btn-primary">{{ editIndex !== null ? 'Update' : 'Add' }}</button>
    </form>

    <ul class="list-group mt-4">
      <li v-for="(product, index) in products" :key="index" class="list-group-item d-flex justify-content-between">
        {{ product.name }}
        <div>
          <button @click="editProduct(index)" class="btn btn-sm btn-warning me-2">Edit</button>
          <button @click="deleteProduct(index)" class="btn btn-sm btn-danger">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const products = ref([])
const form = ref({ name: '' })
const editIndex = ref(null)

const saveProduct = () => {
  if (editIndex.value !== null) {
    products.value[editIndex.value] = { ...form.value }
    editIndex.value = null
  } else {
    products.value.push({ ...form.value })
  }
  form.value.name = ''
}

const editProduct = (index) => {
  form.value = { ...products.value[index] }
  editIndex.value = index
}

const deleteProduct = (index) => {
  products.value.splice(index, 1)
}
</script>
