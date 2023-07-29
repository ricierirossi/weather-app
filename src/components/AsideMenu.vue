<template>
    <aside class="menu">
        <div @click="openCloseMenu">x</div>
        <div class="buttons">
            <SearchLocation />
            <SearchCity />
        </div>
        <div class="cities">
            <div
                class="city"
                :city="'saoPaulo'"
                :lat="-23.55052"
                long="-46.633309"
                @click="chooseCity"
            >
                São Paulo
            </div>
            <div
                class="city"
                :city="'london'"
                :lat="51.507351"
                long="-0.127758"
                @click="chooseCity"
            >
                London
            </div>
            <div class="city" :city="'moscow'" :lat="55.755826" long="37.6173" @click="chooseCity">
                Moscow
            </div>
        </div>
    </aside>
</template>

<script>
import SearchLocation from './SearchLocation.vue'
import SearchCity from './SearchCity.vue'
export default {
    components: { SearchLocation, SearchCity },
    methods: {
        chooseCity(e) {
            const lat = e.target.getAttribute('lat')
            const long = e.target.getAttribute('long')
            this.$emit('choose-city', lat, long)
        },
        openCloseMenu() {
            this.$emit('open-close-menu')
        }
    }
}
</script>

<style>
.menu {
    display: flex;
    flex-direction: column;
    background-color: #1e213a;
}

.buttons {
    display: flex;
    justify-content: space-around;
    margin-top: 40px;
}

.cities {
    display: flex;
    flex-direction: column;
}
</style>
