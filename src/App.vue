<script>
import AppHeader from './components/AppHeader.vue';
import AppSectionSelector from './components/AppSectionSelector.vue';
import AppMain from './components/AppMain.vue';

import {store} from'./data/store';
//import axios from 'axios';

export default{
  name:"App",
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
}
</script>

<template>
  <AppHeader/>
  <AppSectionSelector/>
  <AppMain/>
</template>

<style lang="scss" scoped>

</style>
