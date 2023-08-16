<template>
    <div class="highlight-card">
        <div class="title">UV Index</div>
        <img class="uv-index" :src="icon" width="140" height="140" />
    </div>
</template>

<script>
export default {
    props: ['uVIndex'],
    data: function () {
        return {
            icon: ''
        }
    },
    beforeUpdate() {
        this.icon = '../src/assets/svg/uv-index-' + this.uVIndex.toFixed(0) + '.svg'
    }
}
</script>

<style scoped>
.highlight-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: var(--blue);
}

.title {
    margin-top: 22px;
}
</style>

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

@media (max-width: 375px) {
    .highlight-card {
        width: 328px;
    }
}
</style> -->
