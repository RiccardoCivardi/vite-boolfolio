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

        baseUrl: 'http://127.0.0.1:8000/api/projects',
        projects: [],
        textMaxLength: 100

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

    <ProjectsCard v-for="project in projects" :key="project.id" :project="project"/>

  </div>

</template>


<style lang="scss">

@use './styles/general.scss';

</style>
