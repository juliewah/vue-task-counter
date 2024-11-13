<script setup>
import { ref, computed } from 'vue'
const product = ref({
    name: "精美筆記本",
    description: "高品質紙張，精裝封面",
    price: 100,
    quantity: 0,
    totalPrice: 0,
})

const plus = () => {
    if(product.value.quantity >= 20){
        alert('買太多啦 20個不能再多了')
    } else {
        product.value.quantity++
    }
}
const minus = () => {
    if (product.value.quantity == 0) {
        product.value.quantity = 0
    } else {
        product.value.quantity--
    }
}

const totalPrice = computed(() => {
    return product.value.price * product.value.quantity
})

</script>

<template>
    <div class="card">
        <h2>{{ product.name }}</h2>
        <p>{{ product.description }}</p>
        <p>單價：＄{{ product.price }} </p>
        <p>數量：{{ product.quantity }}</p>
        <p>總價：＄{{ totalPrice }}</p>
        <button @click="minus">-</button>
        <input type="number" v-model="product.quantity">
        <button @click="plus">+</button>
    </div>
</template>

<style>
.card{
    border: 1px solid #a3a3a3;
}
</style>