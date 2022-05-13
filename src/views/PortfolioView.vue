<script setup>
import { ref } from 'vue'
const portfolio = ref(null);

let page = 1;
const nextPage = () => {
  page++;
  console.log('page:',page);
  loadPic(page);
}

const loadPic = (p=1)=>{
  fetch('https://picsum.photos/v2/list?page='+p+'&limit=6')
  .then((res) => res.json())
  .then((json) => {
    portfolio.value = json;
    console.log(json);
  });
}
(loadPic)()
</script>

<template>
<button @click="nextPage">Next Page</button>
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
          <img v-bind:src=" 'https://picsum.photos/id/'+pic.id+'/320/240' " class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">{{ pic.author }}</h5>
            <p class="card-text">{{ pic.url }}</p>
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
