<template>
    <div class="highlight-card">
        <div>Sunset</div>
        <div>{{ sunset }}</div>
        <div>Extra</div>
    </div>
</template>

<script>
export default {
    props: ['sunset']
}
</script>

<style>
.highlight-card {
    background-color: #1e213a;
}
</style>
