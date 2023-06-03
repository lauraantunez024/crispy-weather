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
              Today's forecast <img :src="weatherIcon" :alt="oneCall.current.weather[0].description">

            </h3>
          </template>
          <template v-slot:time>
            <p id="time">{{ now }} </p>
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
              UV: {{ high }}%
            </p>

            <br>
            <p>
              Humidity: {{ humidity }}%
            </p>


          </template>
        </WeatherCard>
      </v-col-9>
      <v-col-9>
        <div v-if="formSubmitted" class="fiveDay">
          <FiveDayForecast v-for="(day, index) in oneCall.daily" :key="index" :weatherSummary="day.summary"
            :weatherDescription="day.weather[0].description" :maxTemp="day.temp.max" :minTemp="day.temp.min"
            :chanceOfRain="day.rain" :humidity="day.humidity">


          </FiveDayForecast>

        </div>

      </v-col-9>
  </v-container>

</div>




          </FiveDayForecast>

        </div>

      </v-col-9>
    </v-container>

  </div>
</template>

<script>
import WeatherCard from '@/components/WeatherCard.vue';
import FiveDayForecast from '@/components/FiveDayForecast.vue'
export default {
  name: 'IndexPage',
  components: {
    WeatherCard,
    FiveDayForecast
  },
  data() {
    return {
      city: '',
      weather: {},
      formSubmitted: false,
      oneCall: {}
    }
  },
  async fetch() {
      this.weather =
        await this.$axios
          .$get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=imperial&appid=cf37cb15ac26f522e8af6d6448e99395`)
          .then(res => (this.weather = res))

      this.oneCall =
        await this.$axios
          .$get(`https://api.openweathermap.org/data/3.0/onecall?lat=${this.weather.coord.lat}&lon=${this.weather.coord.lon}&units=imperial&appid=cf37cb15ac26f522e8af6d6448e99395`)
          .then(res => console.log(res))
          .then(res => (this.oneCall = res))
      this.formSubmitted = true;
  },
  computed: {
    now() {
      return new Date()
    },
    current() {
      return Math.ceil(this.oneCall.current.temp)
    },
    feels_like() {
      return Math.ceil(this.oneCall.current.feels_like.day)
    },
    humidity() {
      return Math.ceil(this.oneCall.current.humidity)
    },
    UV() {
      return Math.ceil(this.oneCall.current.uvi)
    },
    weatherIcon() {
      return "https://openweathermap.org/img/wn/" + this.oneCall.current.weather[0].icon + "@2x.png"
    },


  }
}
</script>


<style  scoped>
.fiveDay {
  display: inline;
}

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

#time {
  font-size: 18px;
}



::v-deep .v-label {
  font-size: .75em;
}
</style>