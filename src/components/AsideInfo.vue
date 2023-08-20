<template>
    <aside class="menu">
        <div class="buttons">
            <SearchButton class="search-button" @click="openCloseMenu" />
            <LocalButton class="local-button" @click="getCoordinates" />
        </div>
        <div class="today">
            <div class="wallpaper">
                <div class="clouds"></div>
                <img class="icon" :src="icon" width="180" height="180" />
            </div>
            <div class="temperature-info">
                <span class="temperature">{{ temperature }}</span>
                <span class="degree" v-if="unit == 'celsius'">°C</span>
                <span class="degree" v-else>°F</span>
            </div>
            <div class="weather">{{ weather }}</div>
            <div class="today-date">
                <span>Today</span>
                <span class="dot"> • </span>
                <span>{{ today }}</span>
            </div>
            <div class="city">
                <span class="material-icons place"> place </span>
                <span class="city-name">{{ cityName }}</span>
            </div>
        </div>
    </aside>
</template>

<script>
import SearchButton from './SearchButton.vue'
import LocalButton from './LocalButton.vue'
export default {
    props: ['temperature', 'weather', 'cityName', 'time', 'temperatureUnit', 'icons'],
    components: { SearchButton, LocalButton },
    data: function () {
        return {
            today: null,
            unit: this.temperatureUnit,
            icon: ''
        }
    },
    methods: {
        formatDate(inputDate) {
            const date = new Date(inputDate)
            const options = { weekday: 'short', day: 'numeric', month: 'short' }
            this.today = date.toLocaleString('en-US', options)
        },
        openCloseMenu() {
            this.$emit('open-close-menu')
        },
        getCoordinates() {
            this.$emit('get-coordinates')
        }
    },
    created() {
        this.formatDate(this.time)
        this.formatDate(this.time)
    },
    watch: {
        temperatureUnit: {
            handler(newUnit) {
                this.unit = newUnit
            }
        },
        icons: {
            handler(newIcon) {
                this.icon = new URL(`../assets/svg/${newIcon}.svg`, import.meta.url).href
            }
        }
    }
}
</script>

<style scoped>
.buttons {
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 18px 12px 0 11px;
    box-sizing: border-box;
}

.today {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.wallpaper {
    position: relative;
    width: 100vw;
}

.clouds {
    background-image: url('../assets/images/Cloud-background.png');
    background-position: center;
    background-size: cover;
    width: 100%;
    height: 326px;
    opacity: 10%;
}

.icon {
    position: absolute;
    left: calc(50% - 125px);
    top: calc(50% - 125px);
    width: 250px;
    height: 250px;
}

.temperature {
    font-size: 144px;
    font-weight: 500;
}

.degree {
    font-size: 48px;
    font-weight: 100;
    color: var(--light-grey);
}

.weather {
    font-size: 36px;
    font-weight: 600;
    color: var(--light-grey);
    margin: 23px 0 48px 0;
}

.today-date {
    font-size: 18px;
    font-weight: 500;
    color: var(--light-grey);
    margin-bottom: 32px;
}

.dot {
    margin: 0 15px;
}

.city {
    display: flex;
    align-items: center;
    font-size: 18px;
    font-weight: 500;
    color: var(--light-grey);
    margin-bottom: 105px;
}

@media (min-width: 576px) {
    .buttons {
        padding: 42px 46px 0 46px;
    }

    .wallpaper {
        width: 100vw;
    }

    .clouds {
        width: 100%;
    }
}

@media (min-width: 768px) {
    .buttons {
        padding-left: 0;
        padding-right: 0;
        justify-content: space-around;
    }
    .today,
    .wallpaper {
        width: 100%;
    }

    .clouds {
        width: 100%;
    }

    .temperature {
        font-size: 80px;
        font-weight: 500;
    }
}

@media (min-width: 1200px) {
    .temperature {
        font-size: 144px;
    }
}
</style>
