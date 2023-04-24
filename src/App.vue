<template>
  <div class="container-fluid">
    <nav class="navbar navbar-dark bg-primary">
      <div class="container-fluid">
        <span class="navbar-brand mb-0 h1">App Title</span>
      </div>
    </nav>
    <div class="container-fluid text-center">
      <div class="row bg-light">
        <div class="col-sm-4 p-2" v-for="item in data.filters">
          {{ item }}
        </div>

      </div>
    </div>
    <div v-if="display">

      <div class="row">
        <div class="col-sm-12 p-2">
          <p> {{ data.header.headerTitle }}
            <br />
            {{ data.header.headerDescription }}
          </p>
        </div>
      </div>
      <div class="container-fluid border-secondary mb-2" v-for="item in data.products">


        <div class="row border" v-if="item.available == true" @click='displayDetailedProduct(item)'>
          <div class="col-sm-2 p-0">
            <img :src="item.imageURL" class="p-3 w-100" />
          </div>
          <div class="col-sm-10 p-0 pt-3">
            <ul class="p-0">
              <li>Name : {{ item.name }}</li>
              <li>{{ item.description }}</li>
              <li>Price : {{ item.price.value + ' ' + item.price.currency }}</li>
              <li>
                <star-rating :rating="item.rating" :read-only="true" :increment="0.01"></star-rating>
              </li>

            </ul>

          </div>

        </div>
        <div class="row border" v-else>

          <div class="col-sm-10 p-0 pt-3">
            <ul class="p-2">
              <li>Name : {{ item.name }}</li>
              <li>{{ item.description }}</li>
              <li>Price : {{ item.price.value + ' ' + item.price.currency }}</li>
              <li>
                <star-rating :rating="item.rating" :read-only="true" :increment="0.01"></star-rating>
              </li>
            </ul>

          </div>
          <div class="col-sm-2">
            <img :src="item.imageURL" class="p-3 w-100 float-end" />
          </div>

        </div>
      </div>
    </div>
    <div v-else>
      <div class="row">
        <div class="col-sm-2 p-0">
          <img :src="product.imageURL" class="p-3 w-100" />
        </div>
        <div class="col-sm-10 p-0 pt-3">
          <ul class="p-0">
            <li>Name : {{ product.name }}</li>
            <li>{{ product.description }}</li>
            <li>Price : {{ product.price.value + ' ' + product.price.currency }}</li>
            <li>
              <star-rating :rating="product.rating" :read-only="true" :increment="0.01"></star-rating>
            </li>

          </ul>

        <p>{{ product.longDescription }}</p>
      
      </div>


      </div>
    </div>
  </div>
</template>

<!-- <script  setup lang="ts"> -->
<script>
import StarRating from 'vue-star-rating'


export default {
  data() {
    return {
      data: {
        'header': { 'headerTitle': '' },
      },
      display: true,
      product: {}
    }
  },
  methods: {
    async getData() {
      const res = await fetch("https://gist.githubusercontent.com/benfranke/c33280a8df5f4f9db2e63ad45cab26a4/raw/f3ad6c00ff520c2667305103d5705bcbb57a7778/products.json");
      const finalRes = await res.json();
      this.data = finalRes;

    },
    displayDetailedProduct(item) {
      this.display = false;
      this.product = item;
    }
  },
  mounted() {
    this.getData()
  },
  components: {
    StarRating
  }
}
</script>

