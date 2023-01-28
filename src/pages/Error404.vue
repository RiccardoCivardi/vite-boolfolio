<script>

  export default {

    name: 'Error404'

  }

</script>


<template>

  <div class="error container-fluid d-flex align-items-center justify-content-center h-100">

    <h1>ERRORE 404!</h1>

  </div>

</template>


<style lang="scss" scoped>

  @use '../styles/partials/vars' as *;

  .error{
    background-color: $light;
    color: white;
  }

</style>
