<template>
  <div id="app">
    <div v-if="!originalDataFromApi && !categories" >
      <div v-if="!errorLoading" >Cargando recursos...</div>
      <div v-else>
        <b-alert show>Error en el servidor. Inténtelo de nuevo más tarde.</b-alert>
      </div>
    </div>
    <div v-else >
      <div>
        Filtre por categoría: 
        <b-form-select v-model="selected" :options="options" />
      </div>
      <div v-for="item in data" :key="item.id" track-by="id" class="grid">
        <b-card
          :title="item.title"
          :img-src="item.image"
          img-height="300"
          img-width="200"
          style="width: 20rem; padding: 1rem;"
        >
          <b-card-text class="font-weight-bold">
            {{ item.price }}$
          </b-card-text>
        </b-card>
      </div>
    </div>
  </div>
</template>
  
<script>
import Vue from 'vue'
import axios from 'axios'
import BootstrapVue from 'bootstrap-vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
Vue.use(BootstrapVue)

export default {
  name: 'List-products',
  data () {
    return {
      originalDataFromApi: null,
      data: null,
      categories: null,
      errorLoading: false,
      options: [
        { text: 'Todo', value: null },
        { text: 'Electrodomesticos', value: 'electronics' },
        { text: 'Joyas', value: 'jewelery' },
        { text: 'Ropa de hombre', value: "men's clothing" },
        { text: 'Ropa de mujer', value: "women's clothing"  }
      ],
      selected: null
    }
  },
  watch: {
    selected() {
      this.changeFilters(this.selected)
    }
  },
  mounted () {
    axios.get('https://fakestoreapi.com/products').then((response) => {
      if (response) {
        this.originalDataFromApi = response.data
        this.data = response.data
      }
    }).catch(function (error) {
      console.log(error)
      this.errorLoading
    })
    axios.get('https://fakestoreapi.com/products/categories').then((response) => {
      if (response) {
        this.categories = response.data
      }
    }).catch(function (error) {
      console.log(error)
      this.errorLoading
    })
  },
  methods: {
    changeFilters (selected) {
      const newArray = []
      if (selected === null) {
        this.data = this.originalDataFromApi
      } else {
        this.originalDataFromApi.forEach(element => {
          if (element.category === selected) {
            newArray.push(element)
          }
        })
        this.data = newArray
      }
    }
  }
}
</script>
  
<style>
  .card {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.2s;
    border-radius: 10px;
    margin: 20px;
  }
  
  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  }
  
  .grid {
    display: inline-block;
  }
</style>
  