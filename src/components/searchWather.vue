<template>
    <div className="row my-4">
       <div className="col-md-6 mx-auto">
          <div className="form-group">
             <input type="search" className="form-control"
             autocomplete="off"
             placeholder="Entre une ville"
            aria-describedby="helpId"
             id="address-input">
          </div>
       </div>
    </div>
</template>

<script>
 import {onMounted,reactive} from "vue";
 import places from "places.js";
 export default {
     emits : ["search-result"],
    setup(props,{emit}){
         const state = reactive({
         appId : "pl84BDTK7HU7",
         apiKey : "671cd803cf905b98ff3217c773e5207a",
     });
     function getPlaces(){
            let placeseAutocomplete = places({
                    appId :state.appId,
                    apiKey : state.apiKey,
                    container : document.querySelector('#address-input')
            });
            placeseAutocomplete.on("change",function($event){
                emit("search-result",$event.suggestion);
            });
     }
     onMounted(()=> {
        getPlaces();
     });
     return {};
    },
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
