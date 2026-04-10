<script setup>
import { ref, onMounted } from 'vue'

const products = ref([])
const loading = ref(true)
const error = ref('')

const fetchProducts = async () => {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('https://kochchakorn.app.n8n.cloud/webhook/Products_67709956')

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`)
    }

    const result = await response.json()
    products.value = result.data || []
  } catch (err) {
    error.value = 'ไม่สามารถดึงข้อมูลได้ กรุณาลองใหม่อีกครั้ง'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchProducts()
})
</script>

<template>
  <div class="container">
    <h1>รายการสินค้า</h1>

    <!-- Loading -->
    <p v-if="loading" class="status loading">กำลังโหลดข้อมูล...</p>

    <!-- Error -->
    <p v-else-if="error" class="status error">{{ error }}</p>

    <!-- No data -->
    <p v-else-if="products.length === 0" class="status empty">ไม่พบข้อมูลสินค้า</p>

    <!-- Product table -->
    <table v-else>
      <thead>
        <tr>
          <th>รหัสสินค้า</th>
          <th>ชื่อสินค้า</th>
          <th>จำนวน</th>
          <th>ราคา</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in products" :key="item.productId">
          <td>{{ item.productId }}</td>
          <td>{{ item.productName }}</td>
          <td>{{ item.quantity }}</td>
          <td>{{ item.price }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5f7fa;
  color: #333;
}

.container {
  max-width: 750px;
  margin: 40px auto;
  padding: 32px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
}

h1 {
  text-align: center;
  margin-bottom: 24px;
  font-size: 1.6rem;
  color: #2c3e50;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  background-color: #db8d34;
  color: #fff;
}

th,
td {
  padding: 12px 16px;
  text-align: left;
}

th {
  font-weight: 600;
  font-size: 0.95rem;
}

tbody tr:nth-child(even) {
  background-color: #f0f4f8;
}

tbody tr:hover {
  background-color: #e8f0fe;
}

td {
  font-size: 0.93rem;
  border-bottom: 1px solid #e9ecef;
}

.status {
  text-align: center;
  padding: 24px;
  font-size: 1rem;
  border-radius: 8px;
}

.loading {
  color: #3498db;
  background-color: #ebf5fb;
}

.error {
  color: #e74c3c;
  background-color: #fdecea;
}

.empty {
  color: #7f8c8d;
  background-color: #f2f3f4;
}
</style>
