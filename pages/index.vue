<script setup lang="ts">
const api_key = '5e393f97f096de59a3a2b8a91749363a';
const wather_url = `https://api.openweathermap.org/data/2.5/weather?q=london&units=metric&appid=5e393f97f096de59a3a2b8a91749363a`
let {data:city,error} = useFetch(`${wather_url }`)
</script>
<template>

    <h1>Hello</h1>
    <p>{{city.main.temp}}</p>
    <p>-----</p>
    <p>{{error}}</p>

</template>