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
  if (products.value[id]. amount> 0) {
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
              <th>Total</th>
            </tr>
          </thead>
          <tbody class="products-item" v-for="(product, index) in products" :key="index">
            <td>
              <div class="product">
                <img :src="product.image" alt="">
                <div class="info">
                  <div class="nome">{{ product.name }}</div>
                 
                </div>
              </div>
            </td>
            <td>{{ product.price }}</td>
            <td>{{ (product.amount * product.price).toFixed(2) }}</td>
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

    <div>
      <section>
        <table>
          <thead>
            <tr>
              <th>Product</th>
              <th>Price</th>
              <th>Total</th>
              <th></th>
            </tr>
          </thead>
          <tbody class="products-item" v-for="(produto, index) in cart" :key="index">
            <td>
              <div class="product">
                <img :src="produto.image" alt="">
                <div class="info">
                  <div class="name">{{ produto.name }}</div>
                </div>
              </div>
            </td>
            <td>{{ produto.price }}</td> 
            <td>{{ (produto.amount * produto.price).toFixed(2) }}</td>
            <td>{{ produto.amount }}</td>
            <td> <button class="buttonCart" @click="removeCart(index)">Remove</button></td>
          </tbody>
        </table>
      </section>
    </div>
  </div>


</template>
<style scoped>

</style>
