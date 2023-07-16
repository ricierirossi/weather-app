<template>
    <div class="highlight-card">
        <div>Sunrise</div>
        <div>{{ sunrise }}</div>
        <div>Extra</div>
    </div>
</template>

<script>
export default {
    props: ['sunrise']
}
</script>

<style>
.highlight-card {
    background-color: brown;
}
</style>
