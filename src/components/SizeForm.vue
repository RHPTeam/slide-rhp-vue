<template>
    <div>
        <input type="number" v-model="singleWidth">
    </div>
</template>

<script>
    export default {
        computed:{
            singleWidth:{
                get(){
                    return this.$store.getters.getWidth;
                },
                set(value){
                    this.$store.dispatch("updateWidth",value);
                }
            }
        }
    }
</script>

<style scoped>

</style>