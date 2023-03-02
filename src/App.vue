<script setup>
import { ref } from 'vue';

// data
const products = ref([
  {
    name: "",
    price: 0,
    qty: 1,
    total: 0
  },
]);

const gradeTotal = ref(0)

// Add form input
function addMore() {
  products.value.push({
    name: "",
    price: 0,
    qty: 1,
    total: 0
  });
}

// Remove 
function remove(index) {
  products.value.splice(index, 1);
}

// update TOTAL product
// func handle Price
function updatePrice(event, index) {
  let product = products.value[index]
  product.total = event.target.value * product.qty
  updateGradeTotal()
}

// func handle Quantity
function updateQuantity(event, index) {
  let product = products.value[index]

  if (event.target.value < 1 & event.target.value != '') {
    alert('Quantity tidak boleh kurang dari 1.')

    product.qty = 1
    event.target.value = 1
  }

  product.total = event.target.value * product.price
  updateGradeTotal()
}

// func handle Grade Total
function updateGradeTotal() {
  console.log('update grade total')
  gradeTotal.value = 0
  products.value.map(item => {
    gradeTotal.value += item.total
  })
}
</script>

<template>
  <div class="container">
    <button class="btn btn-secondary" type="button" @click="addMore()">
      New
    </button>
    <div class="row">
      <div class="col-12 row" v-for="(product, index) in products" :key="index">
        <div class="col-2">
          <label class="form-label">Product name</label>
          <input class="form-control" type="text" v-model="product.name" />
        </div>
        <div class="col-2">
          <label class="form-label">Product price</label>
          <input class="form-control" type="number" @input="updatePrice($event, index)" v-model="product.price" />
        </div>
        <div class="col-2">
          <label class="form-label">Qty</label>
          <input class="form-control" type="number" min="1" v-model="product.qty"
            @input="updateQuantity($event, index)" />
        </div>
        <div class="col-2">
          <label class="form-label">Total</label>
          <input class="form-control" type="number" v-model="product.total" disabled />
        </div>
        <div class="col-4 d-flex align-items-end">
          <button class="btn btn-danger" type="button" v-show="index != 0" @click="remove(index)">
            Delete
          </button>
        </div>
      </div>
      <div class="col-2 offset-6 me-1">
        <label class="form-label">Grade total</label>
        <input class="form-control" type="number" v-model="gradeTotal" disabled />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
