<template>

  <div>


  <v-row class="row ma-5 pa-5">
    <v-col-1>
      <v-form @submit.prevent="$fetch">
        <v-text-field class="ma-0" filled rounded dense height="80" label="Enter City" v-model="city">
        </v-text-field>
      </v-form>
    </v-col-1>
  </v-row>
    <v-container class="content">
      <v-col-9>
        <div class="text-h1 d-flex justify-center title-card">
          {{ weather.name }} 
        </div>
        <br>
        <WeatherCard id="temperature-center" v-if="formSubmitted">
          <template v-slot:header>
            <h3 class="text-h2">
              Today's forecast <img :src="weatherIcon" :alt="weatherDescription">

            </h3>
          </template>
          <template v-slot:time>
             <p>{{ now }} </p>
          </template>
          <template v-slot:main>
            <p>
              Current: {{ current }}°
            </p> 
            <p>
              Feels like: {{ feels_like }}°
            </p>
            <br>
            <p>
              Highest Temperature: {{ high }}°
            </p>
            <p>
              Lowest Temperature: {{ low }}°
            </p>
            <br>
            <p>
              Humidity: {{ weather.main.humidity }}%
            </p> 
            <p>
              Wind speed: {{ weather.wind.speed }}mph
            </p>
       
          </template>
        </WeatherCard>
      </v-col-9>
  </v-container>

</div>




  <!-- 
  <div>

  

    <v-flex>
      <WeatherCard id="humidity">

      </WeatherCard>
    </v-flex>
  </div> -->
</template>

<script>
import WeatherCard from '@/components/WeatherCard.vue';
export default {
  name: 'IndexPage',
  components: {
    WeatherCard
  },
  data() {
    return {
      city: '',
      weather: {},
      formSubmitted: false,
    }
  },
  async fetch() {
    this.weather =
      await this.$axios
        .$get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=imperial&appid=cf37cb15ac26f522e8af6d6448e99395`)
        .then(res => (this.weather = res))
    this.formSubmitted = true;
  },
  computed: {
    now() {
      return new Date()
    },
    current() {
      return Math.ceil(this.weather.main.temp)
    },
    feels_like() {
      return Math.ceil(this.weather.main.feels_like)
    },
    high() {
      return Math.ceil(this.weather.main.temp_max)
    },
    low() {
      return Math.ceil(this.weather.main.temp_min)
    },
    weatherIcon() {
      return "https://openweathermap.org/img/wn/" + this.weather.weather[0].icon + "@2x.png"
    },
    weatherDescription() {
      return "https://openweathermap.org/img/wn/" + this.weather.weather[0].description + "@2x.png"
    }
  }
}
</script>


<style  scoped>

.content {
  margin: auto;
}

.row {
  padding-top: 15px;
}

p#time {
  font-size: 20px;
}

p {
  display: inline-block;
  font-size: 30px;
  margin-right: 15px;
}

#time {
  display: block;
}

.v-text-field {
  font-size: 2em;
  margin-top: 20px;
}




::v-deep .v-label {
  font-size: .75em;
}
</style>