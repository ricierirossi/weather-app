<template>
    <div class="day-card">
        <div class="day">{{ day }}</div>
        <div class="icon">Icon</div>
        <div class="temperatures">
            <div class="max-temperature">
                {{ minTemperature }}
                <span v-if="unit == 'celsius'">°C</span>
                <span v-else>°F</span>
            </div>
            <div class="min-temperature">
                {{ maxTemperature }}
                <span v-if="unit == 'celsius'">°C</span>
                <span v-else>°F</span>
            </div>
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

<style scoped>
.day-card {
    background-color: #1e213a;
    width: 125px;
    height: 177px;
}

.day {
    margin-top: 18px;
    margin-bottom: 10px;
    text-align: center;
}

.icon {
    margin-left: 32px;
    width: 57px;
    height: 62px;
}

.temperatures {
    display: flex;
    justify-content: space-around;
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
