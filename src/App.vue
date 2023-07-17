<template>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />

    <div class="home">
        <AsideInfo
            class="aside-info"
            :temperature="currentWeather.temperature"
            :weather="currentWeather.weathercode"
            :coordinates="coordinates"
            :time="currentWeather.time"
        />
        <ForecastInfo
            class="forecast-info"
            :minTemperature="dailyWeather.temperature_2m_min"
            :maxTemperature="dailyWeather.temperature_2m_max"
            :wind="currentWeather.windspeed"
            :windDirectionCardinal="a"
            :uVIndex="dailyWeather.uv_index_max"
            :sunrise="dailyWeather.sunrise"
            :sunset="dailyWeather.sunset"
        />
    </div>
</template>

<script>
import AsideInfo from './components/AsideInfo.vue'
import ForecastInfo from './components/ForecastInfo.vue'

export default {
    components: { AsideInfo, ForecastInfo },
    data: function () {
        return {
            coordinates: [],
            a: '',
            currentWeather: {
                temperature: null,
                windspeed: null,
                winddirection: null,
                weathercode: null,
                time: null,
                relativeHumidity2m: null,
                visibility: null
            },
            dailyWeather: {
                temperature_2m_min: [],
                temperature_2m_max: [],
                uv_index_max: [],
                sunrise: [],
                sunset: []
            }
        }
    },
    methods: {
        getDataCelsius() {
            fetch(
                'https://api.open-meteo.com/v1/forecast?latitude=-20.9933&longitude=-51.2775&daily=weathercode,temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max,windspeed_10m_max&current_weather=true&timezone=auto'
            )
                .then((resp) => resp.json())
                .then((data) => {
                    this.coordinates[0] = data.latitude
                    this.coordinates[1] = data.longitude
                    this.currentWeather = data.current_weather
                    this.dailyWeather = data.daily
                })
        },
        convertWindDirection(degree) {
            const cardinalPosition = [
                { position: 'North', initialDegree: 0, finalDegree: 22.5 },
                { position: 'Northeast', initialDegree: 22.5, finalDegree: 67.5 },
                { position: 'East', initialDegree: 67.5, finalDegree: 112.5 },
                { position: 'Southeast', initialDegree: 112.5, finalDegree: 157.5 },
                { position: 'Southeast', initialDegree: 157.5, finalDegree: 202.5 },
                { position: 'Southwest', initialDegree: 202.5, finalDegree: 247.5 },
                { position: 'West', initialDegree: 247.5, finalDegree: 292.5 },
                { position: 'Northwest', initialDegree: 292.5, finalDegree: 337.5 },
                { position: 'North', initialDegree: 337.5, finalDegree: 361 }
            ]

            cardinalPosition.forEach((objeto) => {
                if (degree >= objeto.initialDegree && degree < objeto.finalDegree) {
                    console.log(this.a)
                    this.a = objeto.position
                    console.log(this.a)
                }
            })
        }
    },
    mounted() {
        this.getDataCelsius()

        setTimeout(() => {
            this.convertWindDirection(this.currentWeather.winddirection)
        }, 3000)
    }
}
</script>

<style>
.home {
    display: flex;
    color: white;
    height: 100vh;
}

.aside-info {
    flex-basis: 30%;
}

.forecast-info {
    flex-basis: 70%;
}
</style>
