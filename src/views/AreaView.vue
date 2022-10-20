<template>
  <h1>paginas Areas</h1>
  {{codigo}}
</template>

<script>
export default {
     name: 'AreaView',
     data(){
         return {
             codigo : null
         }
     },
     created(){
          this.codigo = this.$route.params.id || 'nuevo';
          console.log(this.$route.params.id,' entro aqui')
     }
}
</script>

<style>

</style>