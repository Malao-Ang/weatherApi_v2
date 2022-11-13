<script setup lang="ts">
const api_key = '5e393f97f096de59a3a2b8a91749363a';

const cokkie = useCookie("city");
if(! cokkie.value){
    cokkie.value = "London"
 }
const search = ref(cokkie.value);
const input = ref("");

const { data: city, error, refresh } = useAsyncData("city", async () => {
    let response;
    try{
        
        response = await $fetch(`https://api.openweathermap.org/data/2.5/weather?q=${search.value}&units=metric&appid=${api_key}`
)
return response

    }catch(error){
        console.log(error);
    cokkie.value = search.value;


    }
    return response;
},{
    watch:[
        search
    ]});


const hendleSearch = () =>{
    search.value = input.value.trim().split(" ").join("+");
    cokkie.value = search.value;
    input.value = "";
    console.log('clickes')
}
</script>
<template>
    <div class="hero min-h-screen bg-base-200">
        <div class="hero-content text-center">
          <div class="max-w-md">
            <h1 class="text-5xl font-bold">{{city.name}}  {{city.main.temp}}°</h1>
            <!-- <p class="py-6">Provident cupiditate voluptatem et in. Quaerat fugiat ut assumenda excepturi exercitationem quasi. In deleniti eaque aut repudiandae et a id nisi.</p> -->
            <div class="form-control">
                <div class="input-group pt-3">
                  <input type="text" placeholder="Search…" class="input input-bordered" v-model="input"/>
                  <button class="btn btn-square " @click="hendleSearch">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" /></svg>
                  </button>
                </div>
              </div>
          </div>
        </div>
      </div>

</template>
<style scoped>
.container{
    height: 100vh;
    margin: 0 auto;
    
}
</style>