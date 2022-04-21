<template>
    <div className="contanier">
       <searchWather @search-result="getWather"/>
       <currentWather :weather="state.weather"/>
       <comingDays :data="state.data"/>
    </div>
</template>

<script>
import {reactive} from "vue";
import searchWather from "./searchWather";
import currentWather from "./currentWather";
import comingDays from "./comingDays";

export default {
   name : "homeWather",
   components : {searchWather,currentWather,comingDays},
  setup(){
    const state = reactive({
        weather : null,
        data : null,
        key : "1d5cfbb4b1ba74f6287033207b5f59d7",
    });
     async function getWather(city)
    {
      const proxy = "https://cors-anywhere.herokuapp.com/";
      const apiUrl = `https://api.darksky.net/forecast/${state.key}/${city.latlng.lat},${city.latlng.lng}?lang=fr&units=ca`;
       const data = await fetch(proxy + apiUrl);
       const resData = await data.json();
       const weatherData = {
           time : resData.currently.time,
           summary : resData.currently.summary,
           icon : `${resData.currently.icon}.png`,
           temperature : `${Math.round(resData.currently.temperature)} °C`,
       };
       state.weather = weatherData;
       state.data = resData.daily.data;
    }
    return {
      getWather,state
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
   body{
       background:#ccc;
       font-family:"Franklin Gothic Medium","Arial Narrow",Arial;
   }
</style>
