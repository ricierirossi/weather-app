<template>
    <div class="highlight-card">
        <div>Wind Status</div>
        <div>{{ wind + ' km/h' }}</div>
        <div>{{ windDirectionCardinal }}</div>
    </div>
</template>

<script>
export default {
    props: ['wind', 'windDirectionCardinal']
}
</script>

<style scoped>
.highlight-card {
    background-color: brown;
}
</style>
