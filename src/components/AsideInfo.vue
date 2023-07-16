<template>
    <aside class="menu">
        <div class="today">
            <SearchButton />
            <LocalButton />
            <div>{{ temperature }}</div>
            <div>{{ weather }}</div>
            <div>Today • Weekenday, Monthday Month</div>
            <div>Local</div>
        </div>
    </aside>
</template>

<script>
import SearchButton from './SearchButton.vue'
import LocalButton from './LocalButton.vue'
export default {
    props: ['temperature', 'weather'],
    components: { SearchButton, LocalButton }
}
</script>

<style>
.menu {
    background-color: #1e213a;
}

.today {
    display: flex;
    justify-content: space-around;
    margin-top: 40px;
}
</style>
