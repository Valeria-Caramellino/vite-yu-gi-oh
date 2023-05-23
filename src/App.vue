<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

import {store} from'./data/store';
import axios from 'axios';

export default{
  
  components:{
    AppHeader,
    AppMain ,
  },
  data(){
    return{
      store,
    }
  },
  mounted(){
    
     axios.get(this.store.urlAPI).then(oggetto => {
      
      this.store.ArrayCards = oggetto.data;
      
      console.log(this.store.ArrayCards)
    }).catch(errore => {

      //In caso di problemi, mostro l'errore in console
      console.error("Qualcosa è andato storto", errore);
      
      this.store.ArrayCards = [];
    
    });
  }
  
}
</script>

<template>
 

  <AppHeader/>
  <AppMain/>
</template>

<style lang="scss" scoped>

</style>
