<script setup>
import { ref } from 'vue'

const portfolio = ref(null);

let page = 1;

const displayPage = ref(page);

const nextPage = (way='') => {
  switch (way){
    case 'next':
      page++;
    break;
    case 'prev':
      page>1 ? page-- : null;
    break;
  }
  displayPage.value = page;
  console.log('page:', page);
  loadPic(page);
}

const loadPic = (page = 1) => {
  fetch('http://127.0.0.1:8000/api/picture?page=' + page + '&limit=6')
    .then((res) => res.json())
    .then((json) => {
      portfolio.value = json;
      console.log(json);
    });
  displayPage.value = page;
}
(loadPic)()
</script>

<template>
  <!-- début container -->
  <div class="container-fluid">
    <div class="row">
      <div class="col-12">
        <h1>Portfolio</h1>
      </div>
    </div>
    <!-- début ligne pagination -->
    <div class="row">
      <div class="col-12">
        <nav aria-label="Page navigation example">
          <ul class="pagination justify-content-center">
            <li v-bind:class="{'page-item': true, 'disabled': displayPage==1?true:false }" >
              <a class="page-link" href="#" @click="nextPage('prev')">Previous</a>
            </li>
            <li class="page-item active"><a class="page-link" href="#" @click="loadPic(displayPage)">{{displayPage}}</a></li>
            <li class="page-item"><a class="page-link" href="#" @click="loadPic(displayPage+1)">{{displayPage+1}}</a></li>
            <li class="page-item"><a class="page-link" href="#" @click="loadPic(displayPage+2)">{{displayPage+2}}</a></li>
            <li class="page-item">
              <a class="page-link" href="#" @click="nextPage('next')">Next</a>
            </li>
          </ul>
        </nav>
      </div>
    </div>
    <!-- fin ligne pagination -->
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
   <!-- début ligne pagination -->
    <div class="row">
      <div class="col-12">
        <nav aria-label="Page navigation example">
          <ul class="pagination justify-content-center">
            <li v-bind:class="{'page-item': true, 'disabled': displayPage==1?true:false }" >
              <a class="page-link" href="#" @click="nextPage('prev')">Previous</a>
            </li>
            <li class="page-item active"><a class="page-link" href="#" @click="loadPic(displayPage)">{{displayPage}}</a></li>
            <li class="page-item"><a class="page-link" href="#" @click="loadPic(displayPage+1)">{{displayPage+1}}</a></li>
            <li class="page-item"><a class="page-link" href="#" @click="loadPic(displayPage+2)">{{displayPage+2}}</a></li>
            <li class="page-item">
              <a class="page-link" href="#" @click="nextPage('next')">Next</a>
            </li>
          </ul>
        </nav>
      </div>
    </div>
    <!-- fin ligne pagination -->
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
