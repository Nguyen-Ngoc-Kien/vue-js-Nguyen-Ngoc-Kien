<script setup>
  import { ref, computed } from 'vue'

  const productData = ref({
    image: 'https://cdn.vjshop.vn/hightech/may-choi-game/ps5/sony-ps-5-1.jpg',
    imageAlt: 'ps5 alt',
    product: 'ps5',
    productLink: 'https://bachtungps.com.vn/may-sony-playstation-5-ps5-1',
    quantity: 10,
    price: 10000,
    discount: 0.2,
    inStock: true,
    classObject: {
      'bg-green': true,
      'bg-blue': false
    }
  })

  function calculateDiscountedPrice() {
    return productData.value.price * (1 - productData.value.discount)
  }

  const productDescription = computed(() => {
    return productData.value.inStock 
      ? `The ${productData.value.product} is currently in stock!`
      : `The ${productData.value.product} is out of stock.`
  })

</script>

<template>
  <div :class="container">
    <h1 :style="{ color: productData.inStock ? 'green' : 'red' }">
      {{ productData.product }}
    </h1>

    <img :src="productData.image" :alt="productData.imageAlt" />

    <div :class="productData.classObject">
      Mua Ngay
    </div>

    <p>Discounted Price: {{ productData.price - productData.price * productData.discount }} $</p>

    <p>{{ productDescription }}</p>

    <p>Original Price: {{ productData.price }} $</p>
  </div>
</template>

<style scoped>
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #f4f4f9;
  }

  .container{
    margin: auto;
    width: 600px;
  }

  .product-container {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 100%;
    text-align: center;
  }

  h1 {
    font-size: 1.8em;
    margin-bottom: 10px;
    text-align: center;
    line-height: 3;
  }

  h1.in-stock {
    color: #28a745; 
  }

  h1.out-of-stock {
    color: #dc3545; 
  }

  img {
    width: 100%;
    max-width: 300px;
    border-radius: 8px;
    margin-bottom: 20px;
    transition: transform 0.3s;
  }

  img:hover {
    transform: scale(1.05);
  }

  .price {
    font-size: 1.5em;
    font-weight: bold;
    color: #333;
    margin: 10px 0;
  }

  .discounted-price {
    font-size: 1.5em;
    font-weight: bold;
    color: #007bff;
    margin: 10px 0;
  }

  p {
    color: #666;
    line-height: 2.6;
    text-align: center;
    font-weight: 600;
    font-size: 16px;
}

  .button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 10px 20px;
    font-size: 1em;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .button:hover {
    background-color: #0056b3;
  }

  .bg-green[data-v-3046c135] {
    background-color: #28a745;
    color: #fff;
    padding: 10px;
    border-radius: 5px;
    margin-top: 10px;
    font-weight: 700;
    font-size: 25px;
    text-align: center;
}

  .bg-blue {
    background-color: #007bff;
    color: #fff;
    padding: 10px;
    border-radius: 5px;
    margin-top: 10px;
  }
</style>