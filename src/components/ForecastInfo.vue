<template>
    <div class="forecast">
        <div class="degrees">
            <CelsiusButton class="celsius" @click="changeUnitToC" />
            <FahrenheitButton @click="changeUnitToF" />
        </div>
        <div class="days-area">
            <DayCard
                day="Tomorrow"
                :minTemperature="minTemperature[1]"
                :maxTemperature="maxTemperature[1]"
                :temperatureUnit="temperatureUnit"
            />
            <DayCard
                :day="day[2]"
                :minTemperature="minTemperature[2]"
                :maxTemperature="maxTemperature[2]"
                :temperatureUnit="temperatureUnit"
            />
            <DayCard
                :day="day[3]"
                :minTemperature="minTemperature[3]"
                :maxTemperature="maxTemperature[3]"
                :temperatureUnit="temperatureUnit"
            />
            <DayCard
                :day="day[4]"
                :minTemperature="minTemperature[4]"
                :maxTemperature="maxTemperature[4]"
                :temperatureUnit="temperatureUnit"
            />
            <DayCard
                :day="day[5]"
                :minTemperature="minTemperature[5]"
                :maxTemperature="maxTemperature[5]"
                :temperatureUnit="temperatureUnit"
            />
        </div>
        <div class="highlight-area">
            <div class="highlight-title">
                <span>Today's Highlights</span>
            </div>
            <div class="highlights">
                <WindStatus :wind="wind" :windDirectionCardinal="windDirectionCardinal" />
                <UVIndex :uVIndex="uVIndex[0]" />
                <SunRise :sunrise="sunrise[0]" />
                <SunSet :sunset="sunset[0]" />
            </div>
        </div>
        <PageFooter />
    </div>
</template>

<script>
import CelsiusButton from './CelsiusButton.vue'
import FahrenheitButton from './FahrenheitButton.vue'
import DayCard from './DayCard.vue'
import WindStatus from './WindStatus.vue'
import UVIndex from './UVIndex.vue'
import SunRise from './SunRise.vue'
import SunSet from './SunSet.vue'
import PageFooter from './PageFooter.vue'

export default {
    props: [
        'days',
        'minTemperature',
        'maxTemperature',
        'wind',
        'weather',
        'windDirectionCardinal',
        'uVIndex',
        'sunrise',
        'sunset',
        'temperatureUnit'
    ],

    components: {
        CelsiusButton,
        FahrenheitButton,
        DayCard,
        WindStatus,
        UVIndex,
        SunRise,
        SunSet,
        PageFooter
    },
    data: function () {
        return {
            day: []
        }
    },
    methods: {
        changeUnitToF() {
            this.$emit('change-unit-to-f')
        },
        changeUnitToC() {
            this.$emit('change-unit-to-c')
        }
    },
    beforeUpdate() {
        this.days.forEach((weekDay) => {
            const date = new Date(weekDay)
            const options = { weekday: 'short', day: 'numeric', month: 'short' }
            this.day.push(date.toLocaleString('en-US', options))
        })
    }
}
</script>

<style>
.forecast {
    background-color: #100e1d;
    padding: 40px 120px 100px 150px;
}

.degrees {
    display: flex;
    justify-content: flex-end;
}

.celsius {
    margin-right: 15px;
}

.days-area {
    display: flex;
    justify-content: space-between;
    margin-top: 30px;
}

.highlight-title {
    margin-top: 72px;
    margin-bottom: 32px;
}

.highlights {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px;
}
</style>
