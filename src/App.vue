<script>
import AppHeader from './components/AppHeader.vue';
import AppSectionSelector from './components/AppSectionSelector.vue';
import AppMain from './components/AppMain.vue';

import {store} from'./data/store';
import axios from 'axios';

export default{
  
  components:{
    AppHeader,
    AppSectionSelector,
    AppMain ,
  },
  data(){
    return{
      store,
    }
  },
  mounted(){
    
     axios.get(this.store.urlAPI).then(oggetto => {

      this.store.ArrayCards.push(oggetto.data)  ;

      console.log(this.store.ArrayCards)
    }).catch(errore => {

      console.error("Qualcosa è andato storto", errore);
      this.store.ArrayCards = [];
    
    });
  }
  
}
</script>

<template>
  <AppHeader/>
  <AppSectionSelector/>
  <AppMain/>
</template>

<style lang="scss" scoped>

</style>
