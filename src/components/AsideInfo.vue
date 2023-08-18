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
                <span class="dot">•</span>
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
    beforeUpdate() {
        this.formatDate(this.time)
        this.icon = '../src/assets/svg/' + this.icons + '.svg'
    },
    mounted() {
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
                this.icon = '../src/assets/svg/' + newIcon + '.svg'
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

<!-- <style scoped>
.menu {
    background-color: #1e213a;
    width: 459px;
}

.buttons {
    display: flex;
    margin: 42px 0 21px 46px;
}

.local-button {
    margin-left: 166px;
}

.today {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.wallpaper {
    position: relative;
}

.clouds {
    background-image: url('../assets/images/Cloud-background.png');
    background-position: center;
    width: 459px;
    height: 376px;
    opacity: 10%;
}

.icon {
    position: absolute;
    left: 105px;
    top: 63px;
    width: 250px;
    height: 250px;
}

.temperature-info {
    margin-top: 33px;
}

.temperature {
    font-weight: 500;
    font-size: 144px;
    line-height: 169.06px;
    color: #e7e7eb;
}

.degree {
    font-weight: 100;
    font-size: 48px;
    color: #a09fb1;
}

.weather {
    margin-top: 87px;
    font-size: 36px;
    font-weight: 600;
    color: #88869d;
}

.today-date {
    margin-top: 87px;
    margin-bottom: 31px;
    font-size: 18px;
    font-weight: 500;
    color: #88869d;
}

.dot {
    margin: 0 16px 0 16px;
}

.city {
    display: flex;
    justify-content: center;
}

.place {
    height: 19px;
    width: 14px;
    color: #88869d;
    margin-right: 15px;
}

.city-name {
    font-weight: 600px;
    font-size: 18px;
    color: #88869d;
}

@media (max-width: 375px) {
    .menu {
        width: 375px;
    }

    .buttons {
        display: flex;
        margin: 29px 12px 0 11px;
    }

    .local-button {
        margin-left: 151px;
    }
    .wallpaper {
        position: relative;
    }

    .clouds {
        background-size: cover;
        width: 375px;
        height: 326px;
    }

    .icon {
        left: 63px;
    }

    .temperature-info {
        margin-top: 0px;
    }

    .weather {
        margin-top: 23px;
    }

    .today-date {
        margin-top: 48px;
    }

    .place {
        margin-bottom: 103px;
    }
}
</style> -->
