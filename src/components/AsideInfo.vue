<template>
    <aside class="menu">
        <div class="buttons">
            <SearchButton @click="openCloseMenu" />
            <LocalButton @click="getCoordinates" />
        </div>
        <div class="today">
            <div>Icon</div>
            <div>{{ temperature }}</div>
            <div>{{ weather }}</div>
            <div>Today • {{ today }}</div>
            <div>{{ cityName }}</div>
        </div>
    </aside>
</template>

<script>
import SearchButton from './SearchButton.vue'
import LocalButton from './LocalButton.vue'
export default {
    props: ['temperature', 'weather', 'cityName', 'time'],
    components: { SearchButton, LocalButton },
    data: function () {
        return {
            today: null
        }
    },
    methods: {
        formatDate(inputDate) {
            const date = new Date(inputDate)
            const options = { weekday: 'short', day: 'numeric', month: 'short' }
            this.today = date.toLocaleString('en-US', options)
        },
        openCloseMenu() {
            this.$emit('open-close-menu')
        },
        getCoordinates() {
            this.$emit('get-coordinates')
        }
    }
    // beforeUpdate() {
    //     this.formatDate(this.time)
    // }
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
