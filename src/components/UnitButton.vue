<template>
    <div>
        <span>{{ unit }}</span>
    </div>
</template>

<script>
export default {
    props: ['unit', 'selected']
}
</script>

<style scoped>
.selected-unit {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #e7e7eb;
    font-size: 18px;
    font-weight: 700;
    color: #110e3c;
}

.unselected-unit {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #585676;
    font-size: 18px;
    font-weight: 700;
    color: #e7e7eb;
}

.selected-unit:hover,
.unselected-unit:hover {
    cursor: pointer;
}
</style>
