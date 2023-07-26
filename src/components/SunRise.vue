<template>
    <div class="highlight-card">
        <div>Sunrise</div>
        <div>{{ sunriseTime }}</div>
    </div>
</template>

<script>
export default {
    props: ['sunrise'],
    data: function () {
        return {
            sunriseTime: null
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

<style>
.highlight-card {
    background-color: #1e213a;
}
</style>
