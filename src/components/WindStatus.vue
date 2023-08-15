<template>
    <div class="highlight-card">
        <div class="title">Wind Status</div>
        <div class="value-unit">
            <span class="value">{{ wind }}</span
            ><span class="unit">km/h</span>
        </div>
        <div class="direction">{{ windDirectionCardinal }}</div>
    </div>
</template>

<script>
export default {
    props: ['wind', 'windDirectionCardinal']
}
</script>

<!-- <style scoped>
.highlight-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #1e213a;
}

.title {
    margin-top: 22px;
}

.value-unit {
    margin-top: 6px;
}
.value {
    font-size: 64px;
    font-weight: 700;
}

.unit {
    font-size: 36px;
    font-weight: 500;
}
.direction {
    margin-top: 32px;
    margin-bottom: 34px;
    font-size: 14px;
    font-weight: 500;
}

@media (max-width: 375px) {
    .highlight-card {
        width: 328px;
    }
}
</style> -->
