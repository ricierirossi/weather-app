<template>
    <div class="highlight-card">
        <div>UV Index</div>
        <div>{{ uVIndex }}</div>
        <div>Extra</div>
    </div>
</template>

<script>
export default {
    props: ['uVIndex']
}
</script>

<style>
.highlight-card {
    background-color: #1e213a;
}
</style>
