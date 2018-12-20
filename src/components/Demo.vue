<template>
    <div>
        <p>My name is :{{getName}}</p>
    </div>
</template>

<script>

export default{
   computed:{
       getName:{
           get(){
               return this.$store.getters.getSlides;
           }, 
       }
   }
}

</script>

<style scoped>

</style>