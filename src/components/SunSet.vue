<template>
    <div class="highlight-card">
        <div>Sunset</div>
        <div>{{ sunsetTime }}</div>
    </div>
</template>

<script>
export default {
    props: ['sunset'],
    data: function () {
        return {
            sunsetTime: null
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

<style scoped>
.highlight-card {
    background-color: #1e213a;
}
</style>
