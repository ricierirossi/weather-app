<template>
    <aside class="menu">
        <div class="material-icons close" @click="openCloseMenu">close</div>
        <div class="buttons">
            <SearchLocation
                class="search-location"
                :searchedLocation="searchedLocation"
                @submit-city="onSubmittedCity"
            />
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
                    <span class="material-icons chevron-right" v-if="hover[0]">
                        chevron_right
                    </span>
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
    display: flex;
    flex-direction: column;
}

.close {
    align-self: flex-end;
    margin: 12px 12px 24px auto;
}

.close:hover {
    cursor: pointer;
}

.search-location {
    box-sizing: content-box;
}

.cities {
    margin: 0 0 0 12px;
    display: flex;
    flex-direction: column;
}

.city {
    display: flex;
    align-items: center;
    width: 339px;
    height: 64px;
    padding-left: 12px;
    font-size: 16px;
    font-weight: 500;
}
.city:hover {
    border: solid 1px var(--darker-grey);
    cursor: pointer;
}

.chevron-right {
    position: absolute;
    left: 334px;
    color: var(--darker-grey);
}

@media (min-width: 768px) {
    .city {
        margin-top: 20px;
        width: 240px;
    }

    .chevron-right {
        left: 230px;
    }
}

@media (min-width: 992px) {
    .city {
        width: 93%;
    }

    .chevron-right {
        left: 334px;
    }
}
</style>
