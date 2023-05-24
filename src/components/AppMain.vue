<script>
import {store} from'../data/store';
import axios from 'axios';
export default{
    name: "AppMain",
    data(){
        return{
         store
        }

    },
    mounted(){
    
    axios.get(this.store.urlAPI).then(oggetto => {

    console.log("Ricevuto:", oggetto.data)
    
    this.store.ArrayCards = oggetto.data  ;

    this.store.loading = false;
    
   })
 },
}
</script>

<template>
 <!--
 <pre>{{ store.ArrayCards.data.length}}</pre> -->
   <div class="container">
        <div class="row" >
            
          <template v-if="store.loading == true">
            <div>La pagina sta caricando</div>
          </template>

          <template v-else>
            <div class="col-12 mx-auto bg-dark text-light p-2">
                Found {{ store.ArrayCards.data.length }} card 
            </div>
            

            <div class="col-10 mx-auto d-flex flex-wrap">
                <template v-for="oggetto in store.ArrayCards.data">
                    <div class="col-2 text-center m-2">
                        <img :src= oggetto.card_images[0].image_url_small alt="">
                        <p>{{ oggetto.name }}</p>
                        <p>{{ oggetto.archetype }}</p> 
                    </div>
                </template> 
            </div>

          </template>
    
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
