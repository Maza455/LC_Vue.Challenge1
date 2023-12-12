<!-- Vue_Challenge1 -->
<template>
  <div class="container">
    <h1>Vue Challenge 1</h1>
    <select v-model="selectedCategory" @change="updateProducts">
      <option value="">Select a category</option>
      <option v-for="category in categories" :key="category">{{ category }}</option>
    </select>

    <input type="text" v-model="searchQuery" placeholder="Search for a product">

    <ul v-if="selectedCategory">
      <li v-for="product in filteredProducts" :key="product.id">
        <img class="img" :src="getImageUrl(product.category)"/>
        {{ product.name }}
      </li>
    </ul>
    <p v-else>Please select a category to view products.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedCategory: '',
      searchQuery: '',
      products: [
        { id: 1, name: 'Zara', category: 'Clothing A' },
        { id: 2, name: 'Lacoste', category: 'Clothing A' },
        { id: 3, name: 'Vertigo', category: 'Clothing A' },
        { id: 4, name: 'Tosoni', category: 'Clothing A' },
        { id: 5, name: 'G-star Raw', category: 'Clothing A' },
        { id: 6, name: 'Replay', category: 'Clothing A' },
        { id: 7, name: 'Rolex', category: 'Watch B' },
        { id: 8, name: 'Casio', category: 'Watch B' },
        { id: 9, name: 'BMW', category: 'Cars C' },
        { id: 10, name: 'Benz', category: 'Cars C' },
        { id: 11, name: 'Bentley', category: 'Cars C' },
        { id: 12, name: 'G-wagon', category: 'Cars C' },
        { id: 10, name: 'Madrid', category: 'Travel D' },
        { id: 11, name: 'Paris', category: 'Travel D' },
        { id: 12, name: 'Mumbai', category: 'Travel D' },
      ],
      categories: ['Clothing A', 'Watch B', 'Cars C', 'Travel D'],
    };
  },
  computed: {
    filteredProducts() {
      let results = this.products;
      if (this.searchQuery) {
        results = results.filter(product => product.name.toLowerCase().includes(this.searchQuery.toLowerCase()));
        if (results.length === 0) {
          alert("Not yet! We don't have the product/s. Come back later.");
        }
      }
      if (this.selectedCategory) {
        results = results.filter(product => product.category === this.selectedCategory);
      }
      return results;
    },
  },
  methods: {
    updateProducts() {
      this.searchQuery = '';
    },
    getImageUrl(category) {
      if (category === 'Clothing A') {
        return 'https://i.postimg.cc/9MP1d4hd/images-9.jpg';
      } else if (category === 'Watch B') {
        return 'https://i.postimg.cc/GpvSSqDY/top-20-watch-brands-lead-1617145581.jpg';
      } else if (category === 'Cars C') {
        return 'https://i.postimg.cc/65Y0qFrY/ogi1-2020-mercedes-amg-g63-018.webp';
      } else {
        return 'https://i.postimg.cc/bNN94bdZ/Kloof-Rd-by-Nico-van-der-Meulen-Architects-07-resize.webp'
      }
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: indigo;
  color: rgb(215, 15, 178);
}

select,
input {
  margin: 10px;
  padding: 5px;
  border-radius: 5px;
  border: none;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  margin: 5px;
}

.img {
  width: 50px;
  height: 50px;
}
</style>
