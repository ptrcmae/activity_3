<template>
  <center>
    <h1 id="shopping-cart-title">Shopping List</h1>
    <div id="app">
      <div class="products">
        <div class="product" v-for="product in products" :key="product.id">
          <h4>
            {{ product.name }} - ₱{{ product.price }}
            <button class="button button1" @click="addToCart(product)">Add to Cart</button>
          </h4>
        </div>
      </div>
      <hr />

      <div class="cart">
        <h2>My Cart</h2>
        <div class="cart-item">
          <center>
          <table>
            <thead>
              <tr>
                <th>Product</th>
                <th>Qty.</th>
                <th></th>
              </tr>
            </thead>
            <tr v-for="(item, index) in cart" :key="item.product.id">
              <td>{{ item.product.name }}</td>
              <td><input type="number" min="1" v-model="item.quantity" @change="updateQuantity(index)"/></td>
              <td><button class="button button2" @click="removeFromCart(index)">Remove</button></td>
            </tr>
          </table>
        </center>
          <br />
          <div><strong>Total: ₱{{ total }}</strong></div>
        </div>
      </div>
    </div>
  </center>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      products: [
        { id: 1, name: "Lotion", price: 300 },
        { id: 2, name: "Body Scrub", price: 120 },
        { id: 3, name: "Hand Cream", price: 99 },
        { id: 4, name: "Eye Cream", price: 350 },
        { id: 5, name: "Toner", price: 100 },
        { id: 6, name: "Facial Wash", price: 129 },
        { id: 7, name: "Mosturizer", price: 249 },
        { id: 8, name: "Sunscreen", price: 200 },
        { id: 9, name: "Serum", price: 175 },
        { id: 10, name: "Sheet Mask", price: 55 },
      ],
      cart: [],
    };
  },
  computed: {
    total() {
      return this.cart.reduce(
        (acc, item) => acc + item.product.price * item.quantity,
        0
      );
    },
  },
  methods: {
    addToCart(product) {
      const existingItem = this.cart.find(
        (item) => item.product.id === product.id
      );
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cart.push({ product: product, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index) {
      const item = this.cart[index];
      if (item.quantity < 1) {
        item.quantity = 1;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
      .products {
        display: justify;
        flex-wrap: center;
      }
      .product {
        margin-right: 10px; /* Add margin between products */
      }
      .cart-item {
        display: justify;
        align-items: center; /* Align items vertically */
        justify-content: space-between;
        margin-bottom: 5px;
      }
      /* Added style for shopping cart title */
      #shopping-cart-title {
        text-align: center;
      }
      input {
        width: 10%;

      }
      .button {
        border: none;
        color: white;
        padding: 5px 15px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 10px;
        margin: 4px 2px;
        cursor: pointer;
      }

      .button1 {
        background-color: #04AA6D;
        border-radius: 12px;
      } 
      .button2 {
        background-color: #f44336;
        border-radius: 12px;
      } 
      table {
        width: 50%;
          display: center;
          border-collapse: collapse;
        }
        th, td {
            border: 1px solid #dddddd;
            padding: 8px;
            text-align: center;
            
        }
        th {
            background-color: #f2f2f2;
        }
</style>
