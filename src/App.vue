<template>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
    <link
        href="https://fonts.googleapis.com/css2?family=Raleway:wght@400;500;700&display=swap"
        rel="stylesheet"
    />

    <div class="home">
        <AsideInfo
            class="aside-info"
            :temperature="currentWeather.temperature"
            :weather="weatherDescription"
            :cityName="cityName"
            :time="currentWeather.time"
        />
        <ForecastInfo
            class="forecast-info"
            :minTemperature="dailyWeather.temperature_2m_min"
            :maxTemperature="dailyWeather.temperature_2m_max"
            :wind="currentWeather.windspeed"
            :windDirectionCardinal="windDirectionCardinal"
            :uVIndex="dailyWeather.uv_index_max"
            :sunrise="dailyWeather.sunrise"
            :sunset="dailyWeather.sunset"
        />
    </div>
</template>

<script>
import AsideInfo from './components/AsideInfo.vue'
import ForecastInfo from './components/ForecastInfo.vue'

// const baseFURL = `https://api.open-meteo.com/v1/forecast?latitude=${this.coordinates.latitude}&longitude=${this.coordinates.longitude}&daily=weathercode,temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max,windspeed_10m_max&current_weather=true&temperature_unit=fahrenheit&timezone=auto`
// const baseCURL = `https://api.open-meteo.com/v1/forecast?latitude=${this.coordinates.latitude}&longitude=${this.coordinates.longitude}&&daily=weathercode,temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max,windspeed_10m_max&current_weather=true&timezone=auto`
// const fahrenheit = '&temperature_unit=fahrenheit'

export default {
    components: { AsideInfo, ForecastInfo },
    data: function () {
        return {
            coordinates: {
                latitude: null,
                longitude: null
            },
            cityName: '',
            currentWeather: {
                temperature: null,
                windspeed: null,
                winddirection: null,
                weathercode: null,
                time: null,
                relativeHumidity2m: null,
                visibility: null
            },
            windDirectionCardinal: '',
            weatherDescription: '',
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
        getLocation() {
            navigator.geolocation.getCurrentPosition((position) => {
                this.coordinates.latitude = position.coords.latitude
                this.coordinates.longitude = position.coords.longitude
            })
        },
        watchLocation() {
            navigator.geolocation.watchPosition((newPosition) => {
                this.coordinates.latitude = newPosition.coords.latitude
                this.coordinates.longitude = newPosition.coords.longitude
            })
        },
        convertLocation(latitude, longitude) {
            fetch(
                `https://api.geoapify.com/v1/geocode/reverse?lat=${latitude}&lon=${longitude}&apiKey=75e439d337d04c80915b5f23c6f31639`
            )
                .then((response) => response.json())
                .then((result) => (this.cityName = result.features[0].properties.city))
        },
        getWeatherData(latitude, longitude) {
            fetch(
                `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&daily=weathercode,temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max,windspeed_10m_max&current_weather=true&timezone=auto`
            )
                .then((resp) => resp.json())
                .then((data) => {
                    this.currentWeather = data.current_weather
                    this.dailyWeather = data.daily
                    this.convertWindDirection(this.currentWeather.winddirection)
                    this.convertWeatherCode(this.currentWeather.weathercode)
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

            cardinalPosition.forEach((positionInfo) => {
                if (degree >= positionInfo.initialDegree && degree < positionInfo.finalDegree) {
                    this.windDirectionCardinal = positionInfo.position
                }
            })
        },
        convertWeatherCode(code) {
            const weatherCodes = [
                { code: 0, description: 'Clear sky' },
                { code: 1, description: 'Mainly clear' },
                { code: 2, description: 'Partly cloudy' },
                { code: 3, description: 'Overcast' },
                { code: 45, description: 'Fog' },
                { code: 48, description: 'Depositing rime fog' },
                { code: 51, description: 'Drizzle: light' },
                { code: 53, description: 'Drizzle: moderate' },
                { code: 55, description: 'Drizzle: dense' },
                { code: 56, description: 'Freezing drizzle: light' },
                { code: 57, description: 'Freezing drizzle: dense' },
                { code: 61, description: 'Rain: slight' },
                { code: 63, description: 'Rain: moderate' },
                { code: 65, description: 'Rain: heavy' },
                { code: 66, description: 'Freezing Rain: light' },
                { code: 67, description: 'Freezing Rain: heavy' },
                { code: 71, description: 'Snow fall: slight' },
                { code: 73, description: 'Snow fall: moderate' },
                { code: 75, description: 'Snow fall: heavy' },
                { code: 77, description: 'Snow grains' },
                { code: 80, description: 'Rain showers: slight' },
                { code: 81, description: 'Rain showers: moderate' },
                { code: 82, description: 'Rain showers: violent' },
                { code: 85, description: 'Snow showers slight' },
                { code: 86, description: 'Snow showers: heavy' },
                { code: 95, description: 'Thunderstorm: slight or moderate' },
                { code: 96, description: 'Thunderstorm with slight hail' },
                { code: 99, description: 'Thunderstorm with heavy hail' }
            ]

            weatherCodes.forEach((codeInfo) => {
                if (code == codeInfo.code) {
                    this.weatherDescription = codeInfo.description
                }
            })
        }
    },
    mounted() {
        this.getLocation()
        this.watchLocation()
    },
    watch: {
        coordinates: {
            handler(newCoordinate) {
                this.getWeatherData(newCoordinate.latitude, newCoordinate.longitude)
                this.convertLocation(newCoordinate.latitude, newCoordinate.longitude)
            },
            deep: true
        }
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
