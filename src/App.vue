<script>

  import axios from 'axios';

  import ProjectsCard from './components/ProjectsCard.vue';

  export default {

    name:'App',

    components: {

      ProjectsCard

    },

    data(){
      return {

        baseUrl: 'http://127.0.0.1:8000/api/',
        projects: [],
        pagination: {
          first: null,
          current: 1,
          prev: null,
          last: null,
          
        }
  
      }
    },

    methods: {

      getApi(page){

        this.pagination.current = page;

        axios.get(this.baseUrl + 'projects', {
          params: {
            page: this.pagination.current
          }   
        })
          .then(results => {

            this.projects = results.data.projects.data;

            this.pagination.first = results.data.projects.first_page_url;
            this.pagination.current = results.data.projects.current_page;
            this.pagination.prev = results.data.projects.prev_page_url;
            this.pagination.last = results.data.projects.last_page;

            console.log(results.data.projects);
          })

      }

    },

    mounted() {
      this.getApi(1)
    }

  }

</script>


<template>

  <h1 class="mt-5 text-center">BENTORNATO VUE &hearts;</h1>
  <h2 class="mt-3 text-center"> CARD DEI PROGETTI</h2>

  <div class="container d-flex flex-wrap ">

    <ProjectsCard v-for="project in projects" :key="project.id" :project="project"/>

  </div>

  <div class="d-flex justify-content-center pagination mb-5">

    <button
      @click="getApi(1)" 
      :disabled="pagination.current === 1"
      class="btn btn-secondary me-2">|&lt; </button>

    <button 
      @click="getApi(pagination.current--)"
      :disabled="pagination.current === 1"
      class="btn btn-secondary me-2">
      &larr;</button>
    
    <button 
      v-for="i in pagination.last" :key="i"
      @click="getApi(i)"
      :disabled="pagination.current === i"
      class="btn btn-secondary me-2">
      {{ i }}</button>
    
    <button
      @click="getApi(pagination.current++)"
      :disabled="pagination.current === pagination.last"
      class="btn btn-secondary me-2">
      &rarr;</button>
    
    <button 
      @click="getApi(pagination.last)"
      :disabled="pagination.current === pagination.last"
      class="btn btn-secondary me-2">
      >|</button>

  </div>

</template>


<style lang="scss">

@use './styles/general.scss';

</style>
