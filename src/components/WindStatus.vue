<template>
    <div class="highlight-card">
        <div>Wind Status</div>
        <div>{{ wind }}</div>
        <div>{{ windDirectionCardinal }}</div>
    </div>
</template>

<script>
export default {
    props: ['wind', 'windDirectionCardinal']
}
</script>

<style>
.highlight-card {
    background-color: brown;
}
</style>
