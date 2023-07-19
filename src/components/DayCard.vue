<template>
    <div class="day-card">
        <div>Day</div>
        <div>Icon</div>
        <div>{{ minTemperature }}</div>
        <div>{{ maxTemperature }}</div>
    </div>
</template>

<script>
export default {
    props: ['minTemperature', 'maxTemperature']
}
</script>

<style>
.day-card {
    background-color: #1e213a;
    width: 120px;
    height: 177px;
}
</style>
