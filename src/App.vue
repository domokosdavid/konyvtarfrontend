<template>
  <div id="app">
    <nav>
      <a href="#">Új könyv</a>
      <a href="https://petrik.hu">Petrik honlap</a>
    </nav>
    <h1 style="text-align: left">Petrik Könyvtár Nyilvántartó</h1>
    <div class="row">
      <div
        class="col-sm-12 col-md-6 col-lg-4"
        v-for="book in books"
        v-bind:key="book.id"
        id="kartya"
      >
        <h3>{{ book.title }}</h3>
        <p>{{ book.author }}</p>
        <p>Kiadási év: {{ book.publish_year }}</p>
        <p>Hossz: {{ book.page_count }} oldal</p>
      </div>
    </div>

    <button @click="loadData">Betöltés</button>
    <footer>
      <p>Készítette: Domokos Dávid</p>
    </footer>
  </div>
</template>

<style>
#kartya {
  border: 1px solid black;
  text-align: left;
  margin-bottom: 1%;
  padding: 1%;
}
nav a {
  padding-left: 30px;
}
footer p{
  float: left;
}
</style>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      mod_new: true,
      saving: false,
      book: {
        title: "",
        author: "",
        publish_year: "",
        page_count: "",
      },
      books: [],
    };
  },
  methods: {
    async loadData() {
      let Response = await fetch("http://127.0.0.1:8000/api/books");
      let data = await Response.json();
      this.books = data;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
