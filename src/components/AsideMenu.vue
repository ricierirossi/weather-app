<template>
    <aside class="menu">
        <div class="buttons">
            <SearchButton />
            <LocalButton />
            <div class="city">São Paulo</div>
            <div class="city">London</div>
            <div class="city">Moscow</div>
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
        }
    },
    beforeUpdate() {
        this.formatDate(this.time)
    }
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
