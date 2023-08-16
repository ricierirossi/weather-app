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
                <WindStatus
                    class="highlights-child"
                    :wind="wind"
                    :windDirectionCardinal="windDirectionCardinal"
                />
                <UVIndex class="highlights-child" :uVIndex="uVIndex[0]" />
                <SunRise class="highlights-child" :sunrise="sunrise[0]" />
                <SunSet class="highlights-child" :sunset="sunset[0]" />
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
.unit {
    display: flex;
    justify-content: center;
    width: 100%;
    margin: 40px 0;
}

.buttons {
    margin-right: 15px;
}

.days-area {
    display: flex;
    flex-direction: column;
    gap: 32px 26px;
    justify-content: space-around;
    flex-wrap: wrap;
}

.highlight-title {
    margin: 32px 0;
    font-size: 24px;
    font-weight: 700;
}

.highlights-child {
    margin-bottom: 32px;
}

.footer {
    margin: 112px 0 24px 0;
}

@media (min-width: 459px) {
    .days-area {
        flex-direction: row;
        gap: 32px 26px;
    }

    .highlights {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 24px;
    }
}

@media (min-width: 768px) {
    .forecast {
        display: flex;
        flex-direction: column;
        padding: 0 125px 0 154px;
    }
    .unit {
        justify-content: flex-end;
    }

    .highlight-title {
        margin-left: -100px;
    }
    .highlights {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 48px;
    }
}
</style>

<!-- <style scoped>
.forecast {
    background-color: #100e1d;
    box-sizing: border-box;
    padding: 40px 120px 100px 154px;
}

.unit {
    display: flex;
    justify-content: flex-end;
    margin-top: 40px;
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
    font-size: 24px;
    font-weight: 700;
}

.highlights {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px;
}

.footer {
    margin-top: 112px;
}

@media (max-width: 375px) {
    .forecast {
        padding: 0;
    }

    .unit {
        display: flex;
        justify-content: center;
        margin-bottom: 20px;
    }

    .days-area {
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 20px 55px 0px 54px;
        margin-top: 30px;
    }

    .highlight-area {
        padding: 0 24px 0 23px;
    }

    .highlight-title {
        margin-top: 19px;
        margin-bottom: 32px;
        font-size: 24px;
        font-weight: 700;
    }

    .highlights {
        display: grid;
        grid-template-columns: 1fr;
        gap: 32px;
    }

    .footer {
        margin-top: 96px;
        margin-bottom: 24px;
        font-size: 14px;
    }
}

/* @media (min-width: 376px) and (max-width: 1366px) {
    .forecast {
        padding: 10px 50px 100px 50px;
    }
} */
</style> -->
