<template>
    <div class="highlight-card">
        <div class="title">Sunrise</div>
        <div class="sunrise">
            <img :src="icon" width="120" height="120" />
            <div>{{ sunriseTime }}</div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['sunrise'],
    data: function () {
        return {
            sunriseTime: null,
            icon: new URL('../assets/svg/sunrise.svg', import.meta.url).href
        }
    },
    methods: {
        getSunrise(time) {
            const moment = new Date(time)
            this.sunriseTime = moment.toLocaleTimeString('en-US')
        }
    },
    watch: {
        sunrise: {
            handler(newSunrise) {
                this.getSunrise(newSunrise)
            }
        }
    }
}
</script>

<style scoped>
.highlight-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: var(--blue);
}

.title {
    margin-top: 22px;
}

.sunrise {
    display: flex;
    align-items: center;
    font-size: 20px;
    padding-right: 10px;
}
</style>
