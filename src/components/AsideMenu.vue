<template>
    <aside class="menu">
        <span class="material-icons close" @click="openCloseMenu"> close </span>
        <div class="buttons">
            <SearchLocation :searchedLocation="searchedLocation" @submit-city="onSubmittedCity" />
        </div>
        <div class="cities">
            <div
                class="city"
                :lat="-23.55052"
                :long="-46.633309"
                @click="chooseCity"
                @mouseenter="hover[0] = true"
                @mouseleave="hover[0] = false"
            >
                São Paulo
                <span class="material-icons chevron-right" v-if="hover[0]"> chevron_right </span>
            </div>
            <div
                class="city"
                :lat="51.507351"
                :long="-0.127758"
                @click="chooseCity"
                @mouseenter="hover[1] = true"
                @mouseleave="hover[1] = false"
            >
                London<span class="material-icons chevron-right" v-if="hover[1]">
                    chevron_right
                </span>
            </div>

            <div
                class="city"
                :lat="55.755826"
                :long="37.6173"
                @click="chooseCity"
                @mouseenter="hover[2] = true"
                @mouseleave="hover[2] = false"
            >
                Moscow<span class="material-icons chevron-right" v-if="hover[2]">
                    chevron_right
                </span>
            </div>
        </div>
    </aside>
</template>

<script>
import SearchLocation from './SearchLocation.vue'

export default {
    components: { SearchLocation },
    props: ['searchedLocation'],
    data: function () {
        return {
            hover: [false, false, false]
        }
    },
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

<style scoped>
.menu {
    background-color: #1e213a;
    height: 672px;
}

.close {
    margin-top: 20px;
    margin-left: 388px;
    text-align: right;
    height: 18px;
    width: 18px;
    color: #e7e7eb;
}

.close:hover {
    cursor: pointer;
}

.cities {
    width: 367px;
    margin-left: 48px;
    margin-top: 58px;
}

.city {
    display: flex;
    align-items: center;
    margin-bottom: 72px;
    padding-left: 12px;
    height: 64px;
    font-size: 16px;
    font-weight: 500;
}

.city:hover {
    border: solid 1px #616475;
    cursor: pointer;
}

.chevron-right {
    position: absolute;
    top: 215px;
    left: 390px;
    color: #616475;
}

@media (max-width: 375px) {
    .menu {
        width: 375px;
    }

    .close {
        margin-left: 339px;
    }

    .cities {
        width: 351px;
        margin-left: 12px;
        margin-top: 38px;
    }

    .chevron-right {
        left: 334px;
    }
}
</style>
