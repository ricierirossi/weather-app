<template>
    <div class="day-card">
        <div>{{ day }}</div>
        <div>Icon</div>
        <div>
            {{ minTemperature }}
            <span v-if="unit == 'celsius'">°C</span>
            <span v-else>°F</span>
        </div>
        <div>
            {{ maxTemperature }}
            <span v-if="unit == 'celsius'">°C</span>
            <span v-else>°F</span>
        </div>
    </div>
</template>

<script>
export default {
    props: ['day', 'minTemperature', 'maxTemperature', 'temperatureUnit'],
    data: function () {
        return {
            unit: this.temperatureUnit
        }
    },
    watch: {
        temperatureUnit: {
            handler(newUnit) {
                this.unit = newUnit
            }
        }
    }
}
</script>

<style>
.day-card {
    background-color: #1e213a;
    width: 120px;
    height: 177px;
}
</style>
