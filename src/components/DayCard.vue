<template>
    <div class="day-card">
        <div>{{ day }}</div>
        <div>Icon</div>
        <div>{{ minTemperature }}</div>
        <div>{{ maxTemperature }}</div>
    </div>
</template>

<script>
export default {
    props: ['day', 'minTemperature', 'maxTemperature']
}
</script>

<style>
.day-card {
    background-color: #1e213a;
    width: 120px;
    height: 177px;
}
</style>
