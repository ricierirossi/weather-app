<template>
    <div class="highlight-card">
        <div class="title">Sunset</div>
        <div class="sunset">
            <img :src="icon" width="120" height="120" />
            <div>{{ sunsetTime }}</div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['sunset'],
    data: function () {
        return {
            sunsetTime: null,
            icon: '../src/assets/svg/sunset.svg'
        }
    },
    methods: {
        getSunset(time) {
            const moment = new Date(time)
            this.sunsetTime = moment.toLocaleTimeString('en-US')
        }
    },
    watch: {
        sunset: {
            handler(newSunset) {
                this.getSunset(newSunset)
            }
        }
    }
}
</script>

<!-- <style scoped>
.highlight-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #1e213a;
}

.title {
    margin-top: 22px;
}

.sunset {
    display: flex;
    align-items: center;
    font-size: 24px;
}

@media (max-width: 375px) {
    .highlight-card {
        width: 328px;
    }
}
</style> -->
