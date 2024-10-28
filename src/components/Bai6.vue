<script setup>
import { ref, computed } from 'vue';

const products = ref([
    { name: 'Sản phẩm 1', price: 100, quantity: 0 },
    { name: 'Sản phẩm 2', price: 200, quantity: 0 },
    { name: 'Sản phẩm 3', price: 300, quantity: 0 },
]);

const totalValue = computed(() => {
    return products.value.reduce((total, product) => {
        return total + product.price * product.quantity;
    }, 0);
});
</script>

<template>
    <div>
        <h1>Giỏ Hàng</h1>
        <ul>
            <li v-for="(product, index) in products" :key="index">
                <span>{{ product.name }} - Giá: {{ product.price }} VNĐ</span>
                <input type="number" v-model.number="product.quantity" min="0" />
            </li>
        </ul>
        <h2>Tổng giá trị giỏ hàng: {{ totalValue }} VNĐ</h2>
    </div>
</template>

<style scoped>
h1 {
    margin-bottom: 20px;
}
h2 {
    margin-top: 20px;
}
li {
    margin-bottom: 10px;
}
input {
    margin-left: 10px;
    width: 50px;
}
</style>