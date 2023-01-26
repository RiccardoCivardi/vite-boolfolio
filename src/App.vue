<script>

  import axios from 'axios';

  export default {

    name:'App',

    data(){
      return {

        baseUrl: 'http://127.0.0.1:8000/api/projects',
        projects: []

      }
    },

    methods: {

      getApi(){

        axios.get(this.baseUrl)
          .then(results => {
            this.projects = results.data.projects.data;
            console.log(this.projects);
          })

      }

    },

    mounted() {
      this.getApi()
    }

    
  
  }

</script>


<template>

  <h1 class="mt-5 text-center">BENTORNATO VUE &hearts;</h1>
  <h2 class="mt-3 text-center"> CARD DEI PROGETTI</h2>

  <div class="container d-flex flex-wrap ">

    <div
      v-for="project in projects" :key="project.id"
      class="card-wrapper">

      <div class="card" style="width: 18rem;">
        <div class="card-body">
          <h5 class="card-title">Progetto: {{project.name}}</h5>
          <h5 v-if="project.type"><span class="badge text-bg-primary">{{project.type.name}}</span></h5>
          
          <div 
            v-if="project.technologies.length"
            class="technologies mb-2">
            <span 
              v-for="technology in project.technologies" :key="technology.id"
              class="badge text-bg-warning me-2 ">{{technology.name}}</span>
          </div>

          <h6 class="card-title">Cliente: {{project.client_name}}</h6>
          <div class="card-text" v-html="project.summary"></div>
        </div>
      </div>

    </div>

  </div>

</template>


<style lang="scss">

@use './styles/general.scss';

.card-wrapper {
  padding: 10px 10px;
}

</style>
