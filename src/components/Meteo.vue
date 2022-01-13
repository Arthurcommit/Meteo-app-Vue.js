<!-- Creation of a Weather App using bootstrap classes and the API website https://openweathermap.org/ -->
<template>

    <div class="container">
        <h1 class="my-4">Meteo App with Vue.js</h1>
            <div class="form-group mb-5">
                <label for="position">Enter a city name</label>
                <input 
                id="position"
                type="text"
                class="form-control"
                v-model="query"
                v-on:keypress.enter="goMeteo">
                <!-- v-on:keypress.enter="goMeteo" = If we press enter... -->
                <!-- I will use two-way data binding to bind input with datas -->
                <!-- keypress = will be activating when I press a touch in the input -->
            </div>
        <div  v-if="display" class="w75 m-auto">
            <h3 class="text-center mb-3">Position : {{weather.name}}</h3>
            <!-- object : 'weather' from datas and 'name' from console.log(this.weather);-->
            <div class="card text-center p-5">
                <p class="texte-affichage">
                    Temperature : {{weather.main.temp.toFixed()}}
                    <!-- toFixed() = method for trim -->
                </p>
                <p class="texte-affichage">
                    Weather : {{weather.weather[0].description}}
                </p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
// Using axios is our tool for doing http querys

export default {
    name:'Meteo',
    data(){
        return{
            query: '', // Request: what we looking for in the input
            weather: undefined, // Weather: datas we received from API
            api_code: 'fb9ad59d8ddf844fe280a8aa02c05bed', // API key we created
            url_research: 'https://api.openweathermap.org/data/2.5/weather?', // URL by city name
            test: false
        }
    },
    methods: {
        goMeteo(){
            // if(e.key == "Enter"){
                axios
                .get(`${this.url_research}q=${this.query}&units=metric&APPID=${this.api_code}&lang=fr`)
                // q(query) = query. It's the city we enter in the input
                // we want units in metrics
                // APPID = secret key API
                .then(reponse => {
                    // console.log(reponse);
                    this.weather = reponse.data
                    console.log(this.weather);
                    // Once we have the reponse, we can add it in the property 'weather'
                })
                this.query = ''
                // It is used to reset the input after we put a city name in the input and keypress enter
                this.display = true
        }
    }

}

</script>

<style scoped>

.texte-affichage {
    font-size: 25px;
    font-weight: 300;
    line-height: 1.2;
}

</style>
