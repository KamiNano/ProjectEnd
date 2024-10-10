<template>
  <div class="product-grid">
    <div v-for="product in products" :key="product.id" class="product-card">
      <img :src="product.image ? product.image : 'https://via.placeholder.com/150' " alt="Product Image" class="product-image" />
      <div class="product-info">
        <h3 class="product-title">Title: {{ product.title }}</h3>
        <p class="product-content">Content: {{ product.content }}</p>
        <p class="product-category">Category: {{ product.category }}</p>
        <button class="edit-button" @click="editBlog(product.id)">แก้ไข Blog</button>
      </div>
    </div>
  </div>
</template>


<script>
import BlogsService from '@/services/BlogsService';

export default {
  data() {
    return {
      products: []
    };
  },
  created() {
    this.fetchProducts();
  },
  methods: {
    fetchProducts() {
      BlogsService.index()
        .then(response => {
          this.products = response.data;
        })
        .catch(error => {
          console.error('Error fetching products:', error);
        });
    },
    editBlog(blogId) {
      this.$router.push({ name: 'blog-edit', params: { blogId: blogId } });
    }
  }
};
</script>

<style>
.product-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: space-around;
}

.product-card {
  border: 1px solid #ddd;
  padding: 16px;
  width: 200px;
  text-align: center;
  background-color: #f9f9f9;
  border-radius: 8px;
}

.product-image {
  width: 100%;
  height: auto;
}

.product-info {
  margin-top: 10px;
}

.product-title {
  font-size: 16px;
  font-weight: bold;
  margin: 8px 0;
}

.product-content, .product-category {
  font-size: 14px;
  margin: 4px 0;
}

.edit-button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 8px 12px;
  cursor: pointer;
  border-radius: 4px;
  margin-top: 8px;
}

.edit-button:hover {
  background-color: #45a049;
}
</style>
