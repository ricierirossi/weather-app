<template>
    <div class="day-card">
        <div class="day">{{ day }}</div>
        <img :src="icons" width="100" height="100" />
        <div class="temperatures">
            <span class="max-temperature">
                {{ minTemperature }}<span v-if="unit == 'celsius'">°C</span><span v-else>°F</span>
            </span>
            <span class="min-temperature">
                {{ maxTemperature }}<span v-if="unit == 'celsius'">°C</span><span v-else>°F</span>
            </span>
        </div>
    </div>
</template>

<script>
export default {
    props: ['day', 'minTemperature', 'maxTemperature', 'temperatureUnit', 'icon'],
    data: function () {
        return {
            unit: this.temperatureUnit,
            icons: ''
        }
    },
    watch: {
        temperatureUnit: {
            handler(newUnit) {
                this.unit = newUnit
            }
        }
    },
    beforeUpdate() {
        this.icons = '../src/assets/svg/' + this.icon + '.svg'
    }
}
</script>

<style scoped>
.day-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: var(--blue);
    width: 120px;
    height: 177px;
}

.day {
    margin-top: 18px;
    text-align: center;
}

.temperatures {
    display: flex;
    justify-content: space-evenly;
    width: 100%;
    font-size: 16px;
    font-weight: 500;
}
.max-temperature {
    color: #e7e7eb;
}

.min-temperature {
    color: #a09fb1;
}
</style>
