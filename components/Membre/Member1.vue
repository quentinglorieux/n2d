<template>
  <body>
    <div class="container">
      <div id="team" class="flex flex-col justify-evenly">
        <div class="flex mx-auto">
          <div class="wrapper flex flex-wrap justify-left gap-5">
            <div v-for="item in listItems" v-bind:key=item.id >      
              <img   :src="item.image"/>

              <div class="overlay flex flex-col">
                  <h3 class="text_overlay px-2 pt-6 text-center">
                 <span> statut</span>
                  </h3>
                  <h4 class="px-2 text-xs text-center">
                   <span> email </span> 
                  </h4>
                  <a  class="flex no-underline hover:no-underline">
                  <button class="but mx-auto mb-2 py-2 px-2 no-underline hover:no-underline focus:bg-white focus:text-blue-800 hover:bg-white hover:text-blue-800"> button </button>
                   </a>
              </div>

            </div>

            </div>
        </div>
      </div>
    </div>
  </body>
</template>

<script setup>
import { ref, onMounted  } from 'vue';
import { Directus } from '@directus/sdk';


const directus = new Directus('https://directus.rubidiumweb.eu');


const listItems = ref([]);

async function publicData() {
	// GET DATA

	// We don't need to authenticate if the public role has access to some_public_collection.
	  const publicData = await directus.items('Members').readByQuery();
    
    
    publicData.data.forEach(element => {
      element.image='https://directus.rubidiumweb.eu/assets/'+element.image
    });
    var L=publicData.data;
    listItems.value = L;

    
    
    
}
publicData();



</script>



<style scoped>
body {
    transition: color 0.5s, background-color 0.5s;
    line-height: 1.5;
    font-family: Lato, Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
      Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
    font-size: 15px;
    text-rendering: optimizeLegibility;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  
  }
  
  .wrapper{
  width: 100%;
  padding-top: 20px;
  justify-content: space-around;
  }
  
  .box-orange{
    min-height: 300px;
  }
  
  .page-content{width: 100%;
  }
  
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: auto;
    width: 100%;
    background-size: cover;
    background-position: center;
    display: block;
    position: relative;
  }
  .container:hover .overlay {
    height: 100%;
  }
  .container img {
    height: 250px;
    width: 190px;
    object-fit: cover;
  }
  
  .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    background-color: rgba(255, 255, 255, 0.63);
    overflow: hidden;
    width: 100%;
    height: 0px;
    transition: .5s ease;
    justify-content: space-around;
  }
  .but{
    color: rgb(5, 65, 131);
    border-bottom-color: rgb(5, 65, 131);
    border-color: rgb(5, 65, 131);
    box-shadow: 0 5px 25px rgba(0, 0, 0, 0.2);
  }
  .but :hover{
    color: rgb(5, 65, 131);
    border-bottom-color: rgb(5, 65, 131);
    border-color: rgb(5, 65, 131);
    box-shadow: 0 5px 25px rgba(0, 0, 0, 0.2);
  }
  
  .page-content a{
    text-decoration: none !important;
  }
  
  .text_overlay {
    display: block;
    position: relative;
    top: 0px;
    right: 0px;
    color: rgb(5, 65, 131);
    font-family: "Roboto", sans-serif;
  font-size: 16px;
  font-weight: 600;
  }
  
  
  .o-wrapper{
      width:80%; 
      margin:auto;
  }
  
  #annuaire_search{
    box-shadow: 0 5px 25px rgba(0, 0, 0, 0.2);
  }
  
  .select_container{
    padding: 5px;
    min-width : 200px;
        -webkit-appearance: button!important;
    appearance: button!important;
  }
  
  .custom-select select {
    box-shadow: 0 5px 25px rgba(0, 0, 0, 0.2)!important;
    -webkit-appearance: button!important;
    appearance: button!important;
    padding: .5rem 1rem!important;
    margin:0px
  }
  
  .rb-container{
    width: 100%;
    height: 250px;
    margin-bottom: 50px;
  }
  .rb-overlay {
    background-color: rgba(255, 255, 255, 0.6);
  }
  
  .rb-font{
    font-family: "Roboto", Sans-serif;
    color: var( --e-global-color-primary );
    font-size: 40px;
  }
  
  
</style>