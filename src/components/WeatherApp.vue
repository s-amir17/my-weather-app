<template>
   <div class="weather">
      <div class="weather__header">
         <i class="fa-solid fa-location-dot" style="color: gray; cursor: pointer"></i>
         <input type="text" placeholder="Your city" v-model.trim="location" @keydown.enter="getWeather" autofocus />
         <button @click="getWeather">
            <img src="@//assets/images/search.png" alt="search" />
         </button>
      </div>
      <p v-if="show">Enter your location!</p>

      <div class="weather__body" v-if="obj.main">
         <img :src="require('/src/assets/images/' + png)" :alt="obj.weather[0].main" />
         <div>
            <h2>{{ Math.trunc(obj.main.temp) }}°c</h2>
            <h3>{{ upperCase(obj.weather[0].description) }}</h3>
         </div>
      </div>

      <div class="weather__footer" v-if="obj.main">
         <div>
            <img src="@//assets/images/humidity.png" alt="." />
            <!-- <i class="fa-solid fa-water"></i> -->
            <div id="inner">
               <span>{{ obj.main.humidity }}%</span>
               Humidity
            </div>
         </div>

         <div>
            <img src="@//assets/images/wind.png" alt="." />
            <!-- <i class="fa-solid fa-wind"></i> -->
            <div id="inner">
               <span>{{ obj.wind.speed.toFixed(1) }} km/h</span>
               Wind speed
            </div>
         </div>
      </div>
   </div>
</template>

<script>
export default {
   props: {
      obj: {
         type: Object,
         default: () => {},
      },
   },

   data() {
      return {
         location: '',
         show: false,
      };
   },

   methods: {
      getWeather() {
         if (this.location == '') {
            this.show = true;
            return;
         } else if (this.location != '') {
            this.show = false;
         }
         this.$emit('getWeather', this.location);
      },
      upperCase(str) {
         return str[0].toUpperCase() + str.slice(1);
      },
   },

   computed: {
      png() {
         if (this.obj.weather) {
            // switch (this.obj.weather[0].main) {
            //    case 'Clear':
            //       return '@//assets/images/clear.png';
            //    case 'Clouds':
            //       return '@//assets/images/clouds.png';
            //    case 'Drizzle':
            //       return '@//assets/images/drizzle.png';
            //    case 'Mist':
            //       return '@//assets/images/mist.png';
            //    case 'Rain':
            //       return '@//assets/images/rain.png';
            //    case 'Snow':
            //       return '@//assets/images/snow.png';
            // }
            if (this.obj.weather[0].main == 'Clear') return 'clear.png';
            else if (this.obj.weather[0].main == 'Clouds') return 'clouds.png';
            else if (this.obj.weather[0].main == 'Drizzle') return 'drizzle.png';
            else if (this.obj.weather[0].main == 'Mist') return 'mist.png';
            else if (this.obj.weather[0].main == 'Rain') return 'rain.png';
            else if (this.obj.weather[0].main == 'Snow') return 'snow.png';
         }
      },
   },
   mounted() {
      // console.log(this.obj);
   },
};
</script>

<style lang="scss" scoped>
.weather {
   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: center;
   padding: 20px;
   border-radius: 15px;
   background-color: #141313;
   width: 400px;
   margin: auto;
   color: aliceblue;
   p {
      font-size: 18px;
      color: crimson;
      font-weight: 600;
      font-style: oblique;
      font-family: Verdana, Geneva, sans-serif;
   }

   &__header {
      display: flex;
      align-items: center;
      gap: 10px;

      input {
         border: none;
         background: none;
         font-size: 22px;
         text-transform: capitalize;
         color: rgb(228, 184, 70);
         font-weight: bold;
         letter-spacing: 1px;
         width: 85%;
         &:focus {
            outline: none;
            // border-bottom: 1px solid goldenrod;
         }
      }
      button {
         cursor: pointer;
         width: 30px;
         height: 30px;
         padding: 5px;
         border: none;
         background: none;
         border-radius: 50%;
         transition: all 0.3s ease-in-out 0s;
         &:hover {
            background-color: gold;
            transform: scale(1.2);
         }
         img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
         }
      }
   }

   &__body {
      margin-bottom: 40px;
      img {
         width: 200px;
      }
      h2 {
         font-size: 40px;
      }
   }

   &__footer {
      width: 100%;
      display: flex;
      justify-content: center;
      gap: 80px;

      div {
         display: flex;
         align-items: center;
         img {
            width: 40px;
            margin-right: 10px;
         }
         #inner {
            display: flex;
            flex-direction: column;
            font-weight: bold;
            span {
               font-size: 25px;
               font-style: italic;
               letter-spacing: 0.7px;
            }
         }
      }
   }
}
</style>
