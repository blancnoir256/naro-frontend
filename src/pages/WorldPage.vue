<script setup lang="ts">
import { ref, onMounted } from 'vue'
const props = defineProps<{ countryName: string , cityName: string }>()
const cityInfo = ref()
const outPuts = ref()
var url:string
onMounted(async () => {
    var countryN = props.countryName
    var cityN = props.cityName
    if(countryN == ""){ countryN = "allCountries" }
    if(cityN == ""){ cityN = "allCities" }
    const res = await fetch('/api/world/' + countryN + '/' + cityN)
    if (res.ok) {
        if (props.countryName != "" && props.cityName != ""){
            cityInfo.value = await res.json()
        }else{
            outPuts.value = await res.json()
        }
    }
})
function reRoad(city_name:string){
    if (props.countryName == ""){
        url = `/world/${city_name}`
    } else  if (props.cityName == "") {
        url = `/world/${props.countryName}/${city_name}`
    }
}
</script>

<template>
  <div>
    <div v-if="outPuts">
        <h1>
            {{ "一覧" }}
        </h1>
        <div v-for="city in outPuts" v-bind:key="city">
            {{reRoad(city)}}
            <li><a v-bind:href = "url">
                {{ city }}
            </a></li>
        </div>
    </div>
    <div v-else>
        <h1>{{ cityName }}</h1>
        <div v-if="cityInfo">{{ cityInfo }}</div>
        <div v-else>
            <h1>
                都市が見つかりませんでした
            </h1>
            <router-link to="/World">
                world
            </router-link></div>
    </div>
  </div>
</template>