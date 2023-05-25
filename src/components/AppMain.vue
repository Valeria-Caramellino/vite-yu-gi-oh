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
            ArchetypeSelect :"Tutti",
            ArrayArchetype:[],
        }

    },
    computed:{ 
        
        
        
    },
    methods:{

        /* cambio api iniziale che le comprende tutte in base al nome del archetype selezionato preso dal v-model della select */
        changeArrayForArchetype(){
            console.log(this.ArchetypeSelect)

            let indirizzo = this.urlArchetypesFilter

           if(this.ArchetypeSelect == "Tutti"){

                indirizzo = this.store.urlAPI

            }else if(this.ArchetypeSelect == this.ArchetypeSelect){

                indirizzo += this.ArchetypeSelect;
            
            }
            /**uso metodo per prendere nuovo indirizzo */
            this.chiamataDati(indirizzo);
        },

        /*prendo api arhetype lo uso per creare array elenco select*/
        generaArchetype(){
                  
            axios.get(this.apiArchetype).then(oggetto => {
                const risposta = oggetto.data          
                this.ArrayArchetype = risposta
            })

        },
        /*creo metodo per chiamare indirizzo api che mi serve*/
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
        /* alla creazione della pagina richiamo i metodi di creazione*/
        this.chiamataDati(this.store.urlAPI);

        this.generaArchetype();
    
   }
}

</script>

<template>
    <main>
        <div class="container ">
            <div class="row  ">
                <div class=" col-12 bg-dark">
                
                    <select  @change="changeArrayForArchetype()" v-model="ArchetypeSelect" >
                        <option selected> Tutti</option>
                        <template  v-for="oggetto in ArrayArchetype">
                            
                            <option >{{ oggetto.archetype_name }}</option>
                        </template>
                    </select>
                </div>
        
            </div>
        
        </div>
        
        
         <!-- <pre>{{ store.ArrayCards.data.length}}</pre> -->
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

    </main>

</template>


 


<style lang="scss" scoped>
//variabile colore
 $oro: darkgoldenrod;
 main{
    width: 100%;
    div{
        background-color: white;
        div.col-2{
        background-color: $oro;
            p{
            color: white;
            }
        }  
    }
 }
 
    
</style>
