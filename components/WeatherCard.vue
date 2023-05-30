<template>
    <v-card class="fiveDayCard" filled dense rounded>
        <v-card-title class="d-flex justify-center" id="card-header">
            <slot name="header"> </slot>
        </v-card-title>
        <v-card-subtitle class="text-subtitle-1 d-flex justify-center">
            <slot name="time" />
        </v-card-subtitle>
        <v-card-text class="text-subtitle-1 d-flex justify-center" id="card-content">
            <slot name="main"> </slot>
        </v-card-text>
    </v-card>
</template>



<script>

export default {
    name: 'WeatherCard',
    data() {
        return {
            city: 'Miami',
            


        }
    },




}



</script>


<style scoped>
.text-subtitle-1 {
    padding: 10px;
}

#card-header {
    text-align: center;
}
</style>
