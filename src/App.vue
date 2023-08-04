<template>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
    <link
        href="https://fonts.googleapis.com/css2?family=Raleway:wght@400;500;700&display=swap"
        rel="stylesheet"
    />

    <div class="home">
        <AsideInfo
            class="aside-info"
            v-if="visible"
            :temperature="currentWeather.temperature"
            :weather="weatherDescription"
            :icons="icons"
            :cityName="cityName"
            :time="currentWeather.time"
            :temperatureUnit="temperatureUnit"
            @get-coordinates="getLocation"
            @open-close-menu="openCloseMenu"
        />
        <AsideMenu
            class="aside-menu"
            v-if="!visible"
            :searchedLocation="searchedLocation"
            @choose-city="getCity"
            @open-close-menu="openCloseMenu"
            @received-city="searchCity"
        />
        <ForecastInfo
            class="forecast-info"
            :days="dailyWeather.time"
            :minTemperature="dailyWeather.temperature_2m_min"
            :maxTemperature="dailyWeather.temperature_2m_max"
            :wind="currentWeather.windspeed"
            :windDirectionCardinal="windDirectionCardinal"
            :uVIndex="dailyWeather.uv_index_max"
            :sunrise="dailyWeather.sunrise"
            :sunset="dailyWeather.sunset"
            :temperatureUnit="temperatureUnit"
            @change-unit-to-f="receiveUnitF"
            @change-unit-to-c="receiveUnitC"
        />
    </div>
</template>

<script>
import AsideInfo from './components/AsideInfo.vue'
import AsideMenu from './components/AsideMenu.vue'
import ForecastInfo from './components/ForecastInfo.vue'

export default {
    components: { AsideInfo, AsideMenu, ForecastInfo },
    data: function () {
        return {
            temperatureUnit: 'celsius',
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
            icons: '',
            windDirectionCardinal: '',
            weatherDescription: '',
            dailyWeather: {
                time: [],
                temperature_2m_min: [],
                temperature_2m_max: [],
                uv_index_max: [],
                sunrise: [],
                sunset: []
            },
            visible: true,
            searchedLocation: ''
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
                navigator.geolocation.clearWatch(1)
            })
        },
        convertLocation(latitude, longitude) {
            fetch(
                `https://api.geoapify.com/v1/geocode/reverse?lat=${latitude}&lon=${longitude}&apiKey=75e439d337d04c80915b5f23c6f31639`
            )
                .then((response) => response.json())
                .then((result) => (this.cityName = result.features[0].properties.city))
        },
        getWeatherData(latitude, longitude, unit) {
            fetch(
                `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&daily=weathercode,temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max,windspeed_10m_max&current_weather=true&temperature_unit=${unit}&timezone=auto`
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
                { code: 0, description: 'Clear sky', icon: 'clear-day' },
                { code: 1, description: 'Mainly clear', icon: 'clear-day' },
                { code: 2, description: 'Partly cloudy', icon: 'partly-cloudy-day' },
                { code: 3, description: 'Overcast', icon: 'overcast' },
                { code: 45, description: 'Fog', icon: 'fog' },
                { code: 48, description: 'Depositing rime fog', icon: 'mist' },
                { code: 51, description: 'Drizzle: light', icon: 'drizzle' },
                { code: 53, description: 'Drizzle: moderate', icon: 'overcast-drizzle' },
                { code: 55, description: 'Drizzle: dense', icon: 'extreme-drizzle' },
                { code: 56, description: 'Freezing drizzle: light', icon: 'sleet' },
                { code: 57, description: 'Freezing drizzle: dense', icon: 'extreme-sleet' },
                { code: 61, description: 'Rain: slight', icon: 'rain' },
                { code: 63, description: 'Rain: moderate', icon: 'overcast-rain' },
                { code: 65, description: 'Rain: heavy', icon: 'extreme-rain' },
                { code: 66, description: 'Freezing Rain: light', icon: 'not-available' },
                { code: 67, description: 'Freezing Rain: heavy', icon: 'not-available' },
                { code: 71, description: 'Snow fall: slight', icon: 'snow' },
                { code: 73, description: 'Snow fall: moderate', icon: 'overcast-snow' },
                { code: 75, description: 'Snow fall: heavy', icon: 'extreme-snow' },
                { code: 77, description: 'Snow grains', icon: 'snow' },
                { code: 80, description: 'Rain showers: slight', icon: 'rain' },
                { code: 81, description: 'Rain showers: moderate', icon: 'overcast-rain' },
                { code: 82, description: 'Rain showers: violent', icon: 'extreme-rain' },
                { code: 85, description: 'Snow showers slight', icon: 'snow' },
                { code: 86, description: 'Snow showers: heavy', icon: 'extreme-snow' },
                {
                    code: 95,
                    description: 'Thunderstorm: slight or moderate',
                    icon: 'thunderstorms'
                },
                {
                    code: 96,
                    description: 'Thunderstorm with slight hail',
                    icon: 'thunderstorms-overcast-snow'
                },
                {
                    code: 99,
                    description: 'Thunderstorm with heavy hail',
                    icon: 'thunderstorms-extreme-snow'
                }
            ]

            weatherCodes.forEach((codeInfo) => {
                if (code == codeInfo.code) {
                    this.weatherDescription = codeInfo.description
                    this.icons = codeInfo.icon
                }
            })
        },
        receiveUnitC() {
            if (this.temperatureUnit === 'fahrenheit') {
                this.temperatureUnit = 'celsius'
            }
        },
        receiveUnitF() {
            if (this.temperatureUnit === 'celsius') {
                this.temperatureUnit = 'fahrenheit'
            }
        },
        getCity(lat, long) {
            this.coordinates.latitude = lat
            this.coordinates.longitude = long
        },
        openCloseMenu() {
            this.visible = !this.visible
        },
        searchCity(city) {
            fetch(
                `https://api.geoapify.com/v1/geocode/search?text=${city}&lang=en&limit=10&type=city&apiKey=75e439d337d04c80915b5f23c6f31639`
            )
                .then((response) => response.json())
                .then((result) => {
                    this.coordinates.latitude = result.features[0].properties.lat
                    this.coordinates.longitude = result.features[0].properties.lon
                })
                .catch(() => console.log('City not foud. Check spelling and try again.'))
            this.visible = !this.visible
        }
    },
    mounted() {
        this.getLocation()
        this.watchLocation()
    },
    watch: {
        coordinates: {
            handler(newCoordinate) {
                this.getWeatherData(
                    newCoordinate.latitude,
                    newCoordinate.longitude,
                    this.temperatureUnit
                )
                this.convertLocation(newCoordinate.latitude, newCoordinate.longitude)
            },
            deep: true
        },
        temperatureUnit: {
            handler(newUnit) {
                this.getWeatherData(this.coordinates.latitude, this.coordinates.longitude, newUnit)
            }
        }
    }
}
</script>

<style scoped>
.home {
    display: flex;
    color: #e7e7eb;
    width: 1440px;
    height: 100vh;
}

.aside-info,
.aside-menu {
    width: 459px;
}

.forecast-info {
    width: 981px;
}
</style>
