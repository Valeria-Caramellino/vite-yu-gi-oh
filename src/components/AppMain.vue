<script>
import {store} from'../data/store';

export default{
    name: "AppMain",
    data(){
        return{
         store
        }
    },
    
}
</script>

<template>
 <!--
 <pre>{{ store.ArrayCards[0].data.length }}</pre>-->
   <div class="container">
        <div class="row" >
           
       
           <div class="col-12 mx-auto bg-dark text-light p-2">Found {{ store.ArrayCards[0].data.length }} card </div>
            <div class="col-10 mx-auto d-flex flex-wrap">
                <template v-for="oggetto in store.ArrayCards[0].data">
                    <div class="col-2 text-center m-2">
                        <img :src= oggetto.card_images[0].image_url_small alt="">
                        <p>{{ oggetto.name }}</p>
                        <p>{{ oggetto.archetype }}</p> 
                    </div>
                </template> 
            </div>
       
          
        </div>
        
    </div>
</template>

<style lang="scss" scoped>
//variabile colore
 $oro: darkgoldenrod;
 div{
    background-color: white;
    div.col-2{
        background-color: $oro;
      p{
        color: white;
    }
 }  
    }
    
</style>
