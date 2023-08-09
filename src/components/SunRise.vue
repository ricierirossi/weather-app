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
            icon: '../src/assets/svg/sunrise.svg'
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
    background-color: #1e213a;
}

.title {
    margin-top: 22px;
}

.sunrise {
    display: flex;
    align-items: center;
    font-size: 24px;
}
</style>
