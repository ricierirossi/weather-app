<template>
    <div class="highlight-card">
        <div>Sunrise</div>
        <div>{{ sunrise }}</div>
        <div>Extra</div>
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
            console.log(moment.toLocaleTimeString('en-US'))
        }
    },
    mounted() {
        this.getSunrise('2023-07-19T05:57')
    }
}
</script>

<style>
.highlight-card {
    background-color: #1e213a;
}
</style>
