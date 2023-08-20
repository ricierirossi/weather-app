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
        this.icon = new URL(`../assets/svg/${this.uVIndex.toFixed(0)}.svg`, import.meta.url).href
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
