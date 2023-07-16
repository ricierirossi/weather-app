<template>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />

    <div class="home">
        <AsideInfo
            class="aside-info"
            :temperature="currentWeather.temperature"
            :weather="currentWeather.weatherCode"
        />
        <ForecastInfo
            class="forecast-info"
            :minTemperature="dailyWeather.temperature_2m_min"
            :maxTemperature="dailyWeather.temperature_2m_max"
            :wind="currentWeather.windSpeed"
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
            currentWeather: {
                temperature: null,
                windSpeed: null,
                windDirection: null,
                weatherCode: null,
                time: null,
                relativeHumidity2m: null,
                visibility: null
            },
            dailyWeather: {
                temperature_2m_min: [],
                temperature_2m_max: []
            }
        }
    },
    methods: {
        getDataCelsius() {
            fetch(
                'https://api.open-meteo.com/v1/forecast?latitude=-23.5475&longitude=-46.6361&hourly=relativehumidity_2m,visibility&daily=temperature_2m_max,temperature_2m_min&current_weather=true&timezone=GMT'
            )
                .then((resp) => resp.json())
                .then((data) => {
                    this.currentWeather = data.current_weather
                    this.dailyWeather = data.daily
                })
        }
    },
    mounted() {
        this.getDataCelsius()
        setTimeout(() => {
            console.log(typeof this.dailyWeather.temperature_2m_max)
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
