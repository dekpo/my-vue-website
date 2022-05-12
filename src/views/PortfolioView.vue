<script setup>
import { ref } from 'vue'

const portfolio = ref(null);
fetch('http://127.0.0.1:8000/api/picture?page=1&limit=6')
  .then((res) => res.json())
  .then((json) => {
    portfolio.value = json;
    console.log(json);
  })
</script>

<template>
<!-- début container -->
  <div class="container-fluid">
    <div class="row">
      <div class="col-12">
        <h1>Portfolio</h1>
      </div>
    </div>
    <!-- début ligne -->
    <div class="row">
      <!-- début colonne -->
      <div v-for="pic in portfolio" class="col-12 col-md-4 mb-3">
        <!-- début card -->
        <div class="card">
          <img v-bind:src="pic.url" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">{{ pic.title }}</h5>
            <p class="card-text">{{ pic.description }}</p>
            <a v-bind:href="pic.url" target="_blank" class="btn btn-primary">Go somewhere</a>
          </div>
        </div>
        <!-- fin card -->
      </div>
      <!-- fin colonne -->
    </div>
    <!-- fin ligne -->
  </div>
<!-- fin container -->
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
