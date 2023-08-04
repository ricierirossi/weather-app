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
            <div class="temperature">
                {{ temperature }}
                <span class="degree" v-if="unit == 'celsius'">°C</span>
                <span class="degree" v-else>°F</span>
            </div>
            <div>{{ weather }}</div>
            <div>Today • {{ today }}</div>
            <div>{{ cityName }}</div>
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
        console.log(this.time)
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
.menu {
    background-color: #1e213a;
    width: 459px;
}

.buttons {
    display: flex;
    margin-top: 42px;
    margin-left: 46px;
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
    opacity: 100%;
}

.temperature {
    font-weight: 100;
    font-size: 48px;
    line-height: 56.35px;
    color: #e7e7eb;
}

.degree {
    font-weight: 500;
    font-size: 14.4px;
    line-height: 169.06px;
    color: #a09fb1;
}
</style>
