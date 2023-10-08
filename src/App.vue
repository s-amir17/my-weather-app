<template>
   <div>
      <h1>Weather App</h1>
      <WeatherApp :obj="obj" @getWeather="getWeather" />
      <NotFound :obj="obj" v-show="obj.cod == '404'" />
   </div>
</template>

<script>
import WeatherApp from './components/WeatherApp.vue';
import NotFound from './components/NotFound.vue';

export default {
   components: { WeatherApp, NotFound },

   data() {
      return {
         obj: {},
         envKey: process.env.VUE_APP_API_KEY,
      };
   },

   methods: {
      async getWeather(location) {
         await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${location}&units=metric&appid=${this.envKey}`)
            .then(res => res.json())
            .then(json => {
               if (json.code == '404') {
               }
               this.obj = json;
               console.log(this.obj);
            })
            .catch(error => console.error(error));
      },
   },
};
</script>

<style lang="scss">
* {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
}
body {
   background-color: darkcyan;
   h1 {
      margin-bottom: 15px;
      color: gold;
   }
}
#app {
   font-family: Avenir, Helvetica, Arial, sans-serif;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   text-align: center;
   padding: 10px 0;
}
</style>
