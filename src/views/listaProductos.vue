<template>
    <div class="container mt-5">
      <h2 class="text-center mb-4">Product List</h2>
      <div class="row">
        <div v-for="product in products" :key="product.id" class="col-md-3 mb-4">
          <!-- Ajuste de tamaño de las columnas a 3 para más productos por fila -->
          <div class="card h-100 shadow-sm">
            <img :src="product.image" class="card-img-top small-image" :alt="product.title" />
            <!-- Clase "small-image" para ajustar el tamaño de la imagen -->
            <div class="card-body">
              <h5 class="card-title">{{ product.title }}</h5>
              <p class="card-text">{{ product.category }}</p>
              <p class="text-muted">{{ formatCurrency(product.price) }}</p>
              <div class="d-flex justify-content-between align-items-center">
                <span class="badge bg-primary">{{ product.rating.rate }} ★</span>
                <small class="text-muted">{{ product.rating.count }} reviews</small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'listProducts',
    data() {
      return {
        products: [],
      };
    },
    mounted() {
      fetch('https://fakestoreapi.com/products')
        .then(response => response.json())
        .then(data => {
          this.products = data;
        });
    },
    methods: {
      formatCurrency(value) {
        return '$' + parseFloat(value).toFixed(2);
      },
    },
  };
  </script>
  
  <style scoped>
  .card-title {
    font-size: 1rem;
    font-weight: bold;
  }
  
  .card-text {
    font-size: 0.85rem;
    color: #555;
  }
  
  .badge {
    font-size: 0.75rem;
  }
  
  .small-image {
    height: 150px; /* Ajuste del tamaño de la imagen */
    object-fit: cover; /* Mantiene el aspecto de la imagen */
  }
  </style>
  