<template>
    <aside class="menu">
        <div class="buttons">
            <SearchButton />
            <LocalButton />
        </div>
        <div class="today">
            <div>Icon</div>
            <div>{{ temperature }}</div>
            <div>{{ weather }}</div>
            <div>{{ time }}</div>
            <div>{{ coordinates }}</div>
        </div>
    </aside>
</template>

<script>
import SearchButton from './SearchButton.vue'
import LocalButton from './LocalButton.vue'
export default {
    props: ['temperature', 'weather', 'coordinates', 'time'],
    components: { SearchButton, LocalButton }
}
</script>

<style>
.menu {
    background-color: #1e213a;
}

.buttons {
    display: flex;
    justify-content: space-around;
    margin-top: 40px;
}

.today {
    display: flex;
    flex-direction: column;
}
</style>
