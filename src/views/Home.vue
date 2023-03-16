<template>
  <h1>Welcome to  home page!</h1>

  <div class="homepage">

   <!--  <div class="homepage__slider">
      <Slider />
    </div> -->

    <div class="homepage__todo">
      <ToDo />
    </div>

    <div class="homepage__contact">
      <Contact />
    </div>

    <div class="homepage__quiz">
      <Quiz />
    </div>
  </div>
</template>

<script>
  import Contact from "../components/Contact.vue";
  //import Slider from "../components/Slider.vue";
  import ToDo from "../components/ToDo.vue";
  import Quiz from "../components/Quiz.vue";

  export default {
    components: {
      Contact,
      ToDo,
      Quiz,
      
    },
  };
</script>

<style scoped>
  .homepage {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 10px;
    
    
  }

 

 /* Default styles */
  h1 {
    font-size: 5rem;
    color: black;
    text-align: center;
  }

  /* Media query for screens smaller than 600px */
  @media only screen and (max-width: 600px) {
    h1{
      font-size: 1rem;
    }
  
  }

 
</style>
