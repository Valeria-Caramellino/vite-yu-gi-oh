<script>
import { store } from '../data/store'
export default{
    name:"AppSectionSelector",
    data(){
        return{
            store
        }
    }
}

</script>

<template>

<div class="container">
    <div class="row">
        <div class="col-2 m-2">
            <select class="form-select" aria-label="Default select example">
                <option selected>Open menu</option>
                
                <template>
                    <option value="1">One</option>
                </template>
                
                
            </select>
        </div>

    </div>

</div>

</template>

<style lang="scss"  scoped>

</style>