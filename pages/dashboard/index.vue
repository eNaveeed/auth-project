<template>

<div class="min-h-screen bg-black">
 <Header/>

</div>

  
</template>

<script>
import Header from "@/components/header/Header.vue";

export default {
  middleware: 'auth',
  components: {
  Header,
  
  
  },
}


</script>

<style>

</style>
