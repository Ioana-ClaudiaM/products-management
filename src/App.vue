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
  </form>

   <template v-bind:class="isShown ? 'products-list' : 'displayNone'">
    <div v-for="product in produse" :key="product" class="list">
      <h2 v-bind:class="product.isAvailable ? 'productAvailable' : 'productNotAvailable'">{{ "Name of product: " + product.name + " category: " +
      product.category + " price: " + product.price + " is available? " + product.isAvailable}}</h2>
      <button @click="deleteProduct()">Delete product</button>
    </div>
   </template>
    
   <div class="categories-list">
    <h2>Lista categorii</h2>
    <select v-model="selectedCategory">
      <option value="electronice">Electronice</option>
      <option value="haine">Haine</option>
      <option value="mancare">Mancare</option>
      <option value="jucarii">Jucarii</option>
    </select>
    
    <div class="products" v-for="product in produse" :key="product"> 
      <h3 v-if="product.category === selectedCategory">{{ product.name }}</h3>
    </div>
   </div>
 
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
      isShown:false,
      selectedCategory:'',
    }
  },
  methods: {
    addProduct(event) {
      event.preventDefault();
      if(this.produs.name !== '' && this.produs.price !== 0)
    {
      this.produse.push({ ...this.produs })
      this.produs = {
        name: '',
        category: '',
        price: 0,
        isAvailable: false,
      };
      this.isShown=true;
    }
    else{
      alert('The name and the price of the product must be completed!')
    }
    },
    deleteProduct(){
      this.produse.splice(this.produse[this.produse.length-1],1)
      if(this.produse.length === 0)
      this.isShown=false
    }
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
  flex-direction: row;
  justify-content: center;
  gap:10%;
  align-items: center;
}

form, .products-list, .categories-list{
  width: fit-content;
  display: flex;
  flex-direction: column;
  padding: 5%;
  backdrop-filter: blur(5px);
  border: 2px solid black;
  border-radius: 20px;
  font-family: 'Poppins';
  font-weight: bold;
  font-size: 1.2rem;
  color: floralwhite;
  -webkit-text-stroke-color: black;
  -webkit-text-stroke-width:0.5px;
}

form input[type=checkbox]{
  width: 5%;
}

form div { 
  display: flex;
  flex-direction: row;
  gap: 5%;
  padding-top:5% ;
}

form button{
  width: 80%;
  margin-left: 10%;
  margin-top:8%;
}

.productAvailable{
color: green;
font-size: 1rem;

}

.productNotAvailable{
  color: red;
  font-size: 1rem;
}

.displayNone{
display:none;
}

.list{
  display: flex;
  flex-direction: row;
}

</style>
