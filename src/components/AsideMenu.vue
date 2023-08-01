<template>
    <aside class="menu">
        <div @click="openCloseMenu">x</div>
        <div class="buttons">
            <SearchLocation :searchedLocation="searchedLocation" @submit-city="onSubmittedCity" />
        </div>
        <div class="cities">
            <div class="city" :lat="-23.55052" :long="-46.633309" @click="chooseCity">
                São Paulo
            </div>
            <div class="city" :lat="51.507351" :long="-0.127758" @click="chooseCity">London</div>
            <div class="city" :lat="55.755826" :long="37.6173" @click="chooseCity">Moscow</div>
        </div>
    </aside>
</template>

<script>
import SearchLocation from './SearchLocation.vue'

export default {
    components: { SearchLocation },
    props: ['searchedLocation'],

    methods: {
        chooseCity(e) {
            const lat = e.target.getAttribute('lat')
            const long = e.target.getAttribute('long')
            this.$emit('choose-city', lat, long)
            this.openCloseMenu()
        },
        openCloseMenu() {
            this.$emit('open-close-menu')
        },
        onSubmittedCity(city) {
            this.$emit('received-city', city)
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
