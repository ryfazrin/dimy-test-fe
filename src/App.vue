<script setup>
import { onMounted, ref } from 'vue';

const products = ref([
  {
    name: "",
    price: 0,
    qty: 0,
    total: 0
  },
]);

function addMore() {
  products.value.push({
    name: "",
    price: 0,
    qty: 0,
    total: 0
  });
}

function remove(index) {
  products.value.splice(index, 1);
}
</script>

<template>
  <div>
    <button type="button" @click="addMore()">
      New
    </button>
    <div>
      <div v-for="(product, index) in products" :key="index">
        <label>Product name {{ product.name }}</label>
        <input type="text" v-model="product.name" />
        <label>Product price</label>
        <input type="number" v-model="product.price" />
        <label>Qty</label>
        <input type="number" v-model="product.qty" />
        <label>Total</label>
        <input type="number" v-model="product.total" disabled />
        <button type="button" @click="remove(index)" v-show="index != 0">
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
