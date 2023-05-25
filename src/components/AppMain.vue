<script>
import {store} from'../data/store';
import axios from 'axios';
export default{
    name: "AppMain",
    data(){
        return{
            store,
            apiArchetype: 'https://db.ygoprodeck.com/api/v7/archetypes.php',
            urlArchetypesFilter: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=',
            selezionatoArchetype :"Tutti",
            ArrayArchetype:[],
            urlApdate:'',
        }

    },
    computed:{ 
        recuperaDati(){
            console.log(this.selezionatoArchetype)

            let indirizzo = this.urlArchetypesFilter

           if(this.selezionatoArchetype == "Tutti"){

                indirizzo = this.store.urlAPI

            }else if(this.selezionatoArchetype == this.selezionatoArchetype){

                indirizzo += this.selezionatoArchetype;
            
            }

            this.chiamataDati(indirizzo);
        } 
        
        
    },
    methods:{
      
        generaArchetype(){
                  
            axios.get(this.apiArchetype).then(oggetto => {
                const risposta = oggetto.data          
                this.ArrayArchetype = risposta
            })

        },
        
        chiamataDati(indirizzo) {

            this.store.loading = true;

            axios.get(indirizzo).then(oggetto => {

            console.log("Ricevuto:", oggetto.data)

            this.store.ArrayCards = oggetto.data  ;

            this.store.loading = false;
            });
        },
      
    },
    mounted(){
    
        this.chiamataDati(this.store.urlAPI);

        this.generaArchetype();
    
   }
}

</script>

<template>

    <div class="container">
        <div class="row">
            <div class="col-2 m-2">
             
                <select  @change="recuperaDati" v-model="selezionatoArchetype" >
                    <option selected> Tutti</option>
                    <template  v-for="oggetto in ArrayArchetype">
                        
                        <option >{{ oggetto.archetype_name }}</option>
                    </template>
                </select>
            </div>
    
        </div>
    
    </div>
    
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
