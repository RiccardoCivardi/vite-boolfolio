<script>
export default {

  name:'ProjectsCard',

  props: {

    project: Object

  },

  data(){
    return{

      textMaxLength: 100

    }
  },

  methods: {

    truncateText(text) {
      if(text.length < this.textMaxLength) return text
      return text.substring(0,this.textMaxLength) + '...';
    }

  }

}
</script>

<template>

  <div class="card-wrapper">

    <div class="card h-100" style="width: 18rem;">
      <div class="card-body">
        <div class="d-flex justify-content-between align-items-center">
          <h5 class="card-title me-3">{{project.name}}</h5>
          <router-link :to="{name: 'project', params: {slug: project.slug}}">
            <i class="fa-regular fa-eye fs-3 text-light"></i>
          </router-link>
        </div>
        <h5 v-if="project.type"><span class="badge text-bg-primary">{{project.type.name}}</span></h5>
        
        <div 
          v-if="project.technologies.length"
          class="technologies mb-2">
          <span 
            v-for="technology in project.technologies" :key="technology.id"
            class="badge text-bg-warning me-2 ">{{technology.name}}</span>
        </div>

        <h6 class="card-title">Cliente: {{project.client_name}}</h6>
        <div class="card-text" v-html="truncateText(project.summary)"></div>
      </div>
    </div>

  </div>
  
</template>

<style lang="scss" scoped>

  .card-wrapper {
    width: calc(100% / 4);
    min-width: 300px;
    padding: 10px 10px;
  }

</style>