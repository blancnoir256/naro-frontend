<script setup lang="ts">
import router from '@/router';
import HelloWorld from '../components/HelloWorld.vue'
var inputCityName = ""
function search(){
    router.push(`/city/${inputCityName}`)
}
</script>
<template>
  <hello-world msg="Hello Vue 3 + Vite" />
  <h1>search a city</h1>
  <input v-model="inputCityName" type="text" />
  <button @click="search">search</button>
</template>