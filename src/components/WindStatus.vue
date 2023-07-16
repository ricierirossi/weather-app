<template>
    <div class="highlight-card">
        <div>Wind Status</div>
        <div>{{ wind }}</div>
        <div>{{ windDirectionPosition }}</div>
    </div>
</template>

<script>
export default {
    props: ['wind', 'winddirection'],
    methods: {
        convertWindDirection(degree) {
            const cardinalPosition = [
                { position: 'North', initialDegree: 0, finalDegree: 22.5 },
                { position: 'Northeast', initialDegree: 22.5, finalDegree: 67.5 },
                { position: 'East', initialDegree: 67.5, finalDegree: 112.5 },
                { position: 'Southeast', initialDegree: 112.5, finalDegree: 157.5 },
                { position: 'Southeast', initialDegree: 157.5, finalDegree: 202.5 },
                { position: 'Southwest', initialDegree: 202.5, finalDegree: 247.5 },
                { position: 'West', initialDegree: 247.5, finalDegree: 292.5 },
                { position: 'Northwest', initialDegree: 292.5, finalDegree: 337.5 },
                { position: 'North', initialDegree: 337.5, finalDegree: 360 }
            ]
            for (const direction in cardinalPosition) {
                if (degree >= direction.initialDegree && degree < direction.finalDegree) {
                    let windDirectionPosition = direction.position
                } else {
                    return 'Unavailable'
                }
            }
        }
    },
    beforeUpdate() {
        this.convertWindDirection(this.winddirection)
    }
}
</script>

<style>
.highlight-card {
    background-color: brown;
}
</style>
