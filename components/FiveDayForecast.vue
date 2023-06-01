<template>
    <div class="container">


        <v-card>
            <v-title>
                {{ dayOfWeek }}
            </v-title>
            <img :src="weatherIcon" :alt="weatherDescription">
            <ul>
                <li>
                    Max temperature: {{ maxTemp }}°
                </li>
                <li>
                    Min temperature: {{ minTemp }}°
                </li>
                <li>
                    {{ weatherSummary }}
                </li>
                <li>
                    Humidity: {{ humidity }}%
                </li>
                <li>
                    Chance of rain: {{ chanceOfRain }}%
                </li>
            </ul>
        </v-card>

    </div>
</template>

<script>
    export default {
        name: 'FiveDayForecast',
        components: {},
        data() {
            return {

            }
        },

        props: {
            weatherIcon: {
                type: String,
                required: false
            },
            weatherDescription: {
                type: String,
                required: false
            },
            dayOfWeek: {
                type: String,
                required: false
            },
            maxTemp: {
                type: Number,
                requred: false
            },
            minTemp: {
                type: Number,
                required: false
            },
            chanceOfRain: {
                type: Number,
                required: false
            },
            humidity: {
                type: Number,
                required: false
            },
            weatherSummary: {
                type: String,
                required: false
            }
        }
        
    }
</script>

<style scoped>

li {
    list-style-type: none;
}


.container {
    display: inline;
}

</style>