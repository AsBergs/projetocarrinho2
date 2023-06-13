<script setup>
import { ref } from 'vue'

const newItem = ref({
  id: 0,
  name: '',
  price: 0,
  amount: 1,
  priceTotal: 0

})

const products = ref([
  {


    id: 1,
    name: 'SPEAK NOW (TAYLOR`S VERSION) CD',
    price: 14.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/files/z0ZgldjYOzHFAkIXofXa_600x.png'

  },
  {
    id: 2,
    name: 'SPEAK NOW (TAYLOR`S VERSION) 3LP VINYL',
    price: 38.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/files/3d1vz27EG2yGTIBXSoFr_600x.png'
  },
  {
    id: 3,
    name: 'SPEAK NOW (TAYLOR`S VERSION) CASSETTE',
    price: 18.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/files/P9OMyRuVtptl46KJEejz_600x.png'
  },
  {

    id: 4,
    name: 'SPEAK NOW (TAYLOR`S VERSION) DIGITAL ALBUM',
    price: 12.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/files/DczpbBwdBLoOceRfaFk2_600x.png'

  },
  {
    id: 5,
    name: 'MIDNIGHTS: JADE GREEN EDITION CD',
    price: 12.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/products/CD2_600x.png?v=1665149108'


  },
  {
    id: 6,
    name: 'MIDNIGHTS: MOONSTONE BLUE EDITION CD',
    price: 12.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/products/CD1_600x.png'

  },
  {
    id: 7,
    name: 'MIDNIGHTS: MAHOGANY EDITION CD',
    price: 12.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/products/CD4_600x.png'

  },
  {
    id: 8,
    name: 'MIDNIGHTS: BLOOD MOON EDITION CD',
    price: 12.99,
    amount: 0,
    image: 'https://cdn.shopify.com/s/files/1/0011/4651/9637/products/CD3_600x.png'

  }
])

const cart = ref([])

function addToCart(index) {
  if (products.value[index].amount > 0) {
    newItem.value.id = products.value[index].id;
    newItem.value.name = products.value[index].name;
    newItem.value.price = products.value[index].price;
    newItem.value.amount = products.value[index].amount;
    newItem.value.image = products.value[index].image;
    newItem.value.priceTotal = products.value[index].amount * products.value[index].price;
    cart.value.push({ ...newItem.value });
  }
  else {
    alert("Select the products first")
  }

}

function removeCart(index) {
  cart.value.splice(index, 1)
}

function takeOut(id) {
  if (products.value[id].amount > 0) {
    products.value[id].amount--;
  }
}



</script>
<template>
  <ul class="products-main">
    <h1>Taylor Swift Store</h1>
    <h2>Products</h2>

    <div>
      <section>
        <table>
          <thead>
            <tr>
              <th>Product</th>
              <th>Price</th>
              <th>Amount</th>
            </tr>
          </thead>
          <tbody class="products-item" v-for="(product, index) in products" :key="index">
            <td>
              <div class="product">
                <img :src="product.image" alt="">
                <div>
                  <div class="nome">{{ product.name }}</div>
                </div>
              </div>
            </td>
            <td>{{ product.price }}</td>

            <td>
              <div class="button">
                <button class="buttons" @click="product.amount++">+</button>
                <p>{{ product.amount }}</p>
                <button class="buttons" @click="takeOut(product.id - 1)">-</button>
              </div>
            </td>
            <td><button class="buttonCart" @click="addToCart(index)">Add To Cart</button></td>
          </tbody>
        </table>
      </section>
    </div>
   
  </ul>
  <div class="cart">
    <h2>Cart</h2>
    <p v-if="cart.length === 0">Your Cart is empty</p>

    <div v-else>
      <section>
        <table>
          <thead>
            <tr>
              <th>Product</th>
              <th>Total</th>
              <th></th>
            </tr>
          </thead>
          <tbody class="products-item" v-for="(product, index) in cart" :key="index">
            <td>
              <div class="product">
                <img :src="product.image" alt="">
                <div class="info">
                  <div class="name">{{ product.name }}</div>
                </div>
              </div>
            </td>
            
            <td>{{ (product.amount * product.price).toFixed(2) }}</td>
                <td><button class="buttons" @click="product.amount++">+</button></td> 
                <td>{{ product.amount }}</td>
               <td><button class="buttons" @click="product.amount > 1 && product.amount--">-</button></td> 
            <td> <button class="buttonCart" @click="removeCart(index)">Remove</button></td>
          </tbody>
        </table>
      </section>
    </div>
  </div>
 
</template>
<style scoped>



.products-main {
  width: 1000px;
  align-items: center;
  font-size: 18px;
  background-color: rgb(112, 9, 138);
  padding: 30px;
  margin: 10px 5px;
  border-radius: 10px;  
  grid-template-columns: 3fr 1fr;
}

.button {
  background-color: rgb(112, 9, 138);
  align-items: center; 
  border-radius: 20px;
  padding: 0 10px;
  justify-content: space-around;
  min-width: 60px;
  margin: 10px 5px;
  display: inline-flex;
}

.buttonCart {
  border-radius: 30px;
  font-weight: bold;
  font-size: 16px;
  padding: 7px 20px;
  margin: 10px 5px;
  background-color: blueviolet; 
  width: 100px;
}

.buttons {
  background: rgb(112, 9, 138);
  border: none;
  align-items: center;
  font-size: 30px;
  margin: 10px 5px;
  padding: 0 10px;
}

h1{
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

h2 {
  text-align: center;
  font-family:'Times New Roman', Times, serif;
  font-size: 30px;
}

.products-main .products-item,
td {
  background-color: rgb(183, 19, 224);
  position: relative;
  width: 100%;
  margin: 40px 0;
  align-items: center;
  font-size: 20px;
  justify-content: space-around;
}
.cart {
  font-size: 28px;
  background-color: rgb(121, 4, 150);
  border-radius: 10px;
  border-width:  35px solid rgb(51, 5, 63);
  width: 1000px;
  height: auto;
  padding: 30px
}


.item {
  background-color: purple;
  position: relative;
  width: 100%;
  margin: 30px 0;
  border-radius: 8px;
  justify-content: space-around;
  align-items: center;
}

table {
  border-spacing: 0 30px;
}
tr {
  border-bottom: 3px;
  border-color: blueviolet;
}
th {
  text-align: left;
  font-size: 25px;
  font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}

.name {
  align-items: center;
  display: flex;
}

.product {
  align-items: center;
  display: flex;
}
img{
  max-width: 150px;
} 

p{
  font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}

</style>
