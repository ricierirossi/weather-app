<template>
    <div class="forecast">
        <div class="unit">
            <UnitButton
                unit="°C"
                :class="selected ? 'selected-unit' : 'unselected-unit'"
                class="buttons"
                @click="changeUnitToC"
            />
            <UnitButton
                unit="°F"
                :class="!selected ? 'selected-unit' : 'unselected-unit'"
                @click="changeUnitToF"
            />
        </div>
        <div class="days-area">
            <DayCard
                day="Tomorrow"
                :minTemperature="minTemperature[1]"
                :maxTemperature="maxTemperature[1]"
                :temperatureUnit="temperatureUnit"
                :icon="nextDaysIcons[1]"
            />
            <DayCard
                :day="day[2]"
                :minTemperature="minTemperature[2]"
                :maxTemperature="maxTemperature[2]"
                :temperatureUnit="temperatureUnit"
                :icon="nextDaysIcons[2]"
            />
            <DayCard
                :day="day[3]"
                :minTemperature="minTemperature[3]"
                :maxTemperature="maxTemperature[3]"
                :temperatureUnit="temperatureUnit"
                :icon="nextDaysIcons[3]"
            />
            <DayCard
                :day="day[4]"
                :minTemperature="minTemperature[4]"
                :maxTemperature="maxTemperature[4]"
                :temperatureUnit="temperatureUnit"
                :icon="nextDaysIcons[4]"
            />
            <DayCard
                :day="day[5]"
                :minTemperature="minTemperature[5]"
                :maxTemperature="maxTemperature[5]"
                :temperatureUnit="temperatureUnit"
                :icon="nextDaysIcons[5]"
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
        <PageFooter class="footer" />
    </div>
</template>

<script>
import UnitButton from './UnitButton.vue'
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
        'temperatureUnit',
        'nextDaysIcons'
    ],

    components: {
        UnitButton,
        DayCard,
        WindStatus,
        UVIndex,
        SunRise,
        SunSet,
        PageFooter
    },
    data: function () {
        return {
            day: [],
            selected: true
        }
    },
    methods: {
        changeUnitToC() {
            this.$emit('change-unit-to-c')
            this.selected = !this.selected
        },

        changeUnitToF() {
            this.$emit('change-unit-to-f')
            this.selected = !this.selected
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

<style scoped>
.forecast {
    background-color: #100e1d;
    box-sizing: border-box;
    padding: 40px 120px 100px 154px;
}

.unit {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 66px;
}

.buttons {
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

.highlight-title > span {
    font-size: 24px;
    font-family: 700;
}

.highlights {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px;
}

.footer {
    margin-top: 112px;
}
</style>
