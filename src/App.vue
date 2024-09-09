<template>

  <form>
    <div>
      <label for="name">Name:</label>
      <input type="text" v-model="produs.name" id="name">
    </div>

    <div>
      <label for="category">Category:</label>
      <select name="category" id="category" v-model="produs.category">
        <option value="electronice">Electronice</option>
        <option value="haine">Haine</option>
        <option value="mancare">Mancare</option>
        <option value="jucarii">Jucarii</option>
      </select>
    </div>

    <div>
      <label for="price">Price:</label>
      <input type="number" v-model="produs.price" id="price">
    </div>

    <div>
      <label for="isAvailable">Is available?</label>
      <input type="checkbox" v-model="produs.isAvailable" id="isAvailable" true-value="Yes, it is available."
        false-value="No, it is not available.">
    </div>

    <button v-on:click="addProduct">Adauga produsul in lista</button>

    <div v-for="product in produse" :key="product">
      <h2 v-bind:class="!isAvailable ? 'productAvailable' : 'productNotAvailable'">{{ "Name of product: " + product.name + " category: " +
      product.category + " price: " + product.price + " is available? " + product.isAvailable}}</h2>
    </div>
  </form>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      produse: [],
      produs: {
        name: '',
        category: '',
        price: 0,
        isAvailable: false,
      },
    }
  },
  methods: {
    addProduct(event) {
      event.preventDefault();
      this.produse.push({ ...this.produs })
      this.produs = {
        name: '',
        category: '',
        price: 0,
        isAvailable: false,
      };
    },
  },
}

</script>

<style>
#app {
  text-align: center;
  background-image: url('../public/joyful-little-girl-sitting-shopping-cart.jpg');
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

form {
  width: fit-content;
  display: flex;
  flex-direction: column;
  padding: 5%;
  backdrop-filter: blur(5px);
  border: 2px solid black;
  border-radius: 20px;
  font-family: 'Poppins';
  font-weight: bold;
  font-size: 1.5rem;
  color: floralwhite;
  -webkit-text-stroke-color: black;
  -webkit-text-stroke-width:0.5px;
}

form div {
  display: flex;
  flex-direction: row;
  gap: 5%;
  padding-top:5% ;
}

.productAvailable{
color: green;
}

.productNotAvailable{
  color: red;

}

</style>
