<template>
    <div class="highlight-card">
        <div>Wind Status</div>
        <div>{{ wind }}</div>
        <div>{{ winddirectioncardinal }}</div>
    </div>
</template>

<script>
export default {
    props: ['wind', 'winddirectioncardinal']
}
</script>

<style>
.highlight-card {
    background-color: brown;
}
</style>
