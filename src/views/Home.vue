<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Welcome to checkroof
        </p>
        <p class="subtitle">
          Discover what your roof can do for you
        </p>
      </div>
    </section>
    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest Products</h2>
      </div>
    <ProductBox v-for="product in latestProducts" v-bind:key="product.id" v-bind:product="product" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import axios from 'axios'
import ProductBox from '@/components/ProductBox'

export default {

  name: 'Home',
  data(){
    return {
      latestProducts:[]
    }
  },
  components:{
    ProductBox
  },
  mounted(){
    this.getLatestProducts()
    document.title = 'Home | Checkroof'
  },
  methods:{
    async getLatestProducts(){
      this.$store.commit('setIsLoading', true)
      await axios.get('/api/v1/latest-products/')
      .then((response)=>{
        this.latestProducts = response.data
      })
      .catch((error)=>{
        console.log(error)
      })
      this.$store.commit('setIsLoading', false)
    }
  }
}
</script>

<style scoped>
  .image {
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
</style>