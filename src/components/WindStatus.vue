<template>
    <div class="highlight-card">
        <div>Wind Status</div>
        <div>{{ wind }}</div>
        <div>Extra</div>
    </div>
</template>

<script>
export default {
    props: ['wind']
}
</script>

<style>
.highlight-card {
    background-color: brown;
}
</style>
