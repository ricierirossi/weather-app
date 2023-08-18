<template>
    <div class="local">
        <span class="material-icons">gps_fixed</span>
    </div>
</template>

<script>
export default {}
</script>

<style scoped>
.local {
    background-color: var(--dark-grey);
    box-shadow: 0px 4px 4px 0px var(--black-shadow);
    border-radius: 50%;
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.local:hover {
    cursor: pointer;
}
</style>
