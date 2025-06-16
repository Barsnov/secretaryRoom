<template>
  <back :images="images"></back>
</template>

<script>
  import Back from '@/components/Background.vue'

  export default {
    components: {
      Back
    },

    data(){
      return {
        images: []
      }
    },

    methods: {
      async getImages(){
        try{
          const response = await fetch('/public/imagesBack.txt');
          this.images = await response.json();
          if (!response.ok) new Error('Интернет подключи');
        } catch (error){
          console.error('Файл умер при извлечении...', error);
        }
      }
    },

    mounted() {
      this.getImages()
    }
  }
</script>

<style>
    body, html{
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
    }
</style>