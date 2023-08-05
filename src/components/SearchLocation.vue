<template>
    <form @submit.prevent="submitCity">
        <input class="search-box" placeholder="search location" type="text" v-model="city" />
        <input class="submit-button" type="submit" />
    </form>
</template>

<script>
export default {
    props: ['searchedLocation'],
    data: function () {
        return {
            city: ''
        }
    },
    methods: {
        submitCity() {
            const city = this.city
            this.$emit('submit-city', city)
        }
    }
}
</script>

<style scoped>
.submit-button {
    all: unset;
}
</style>
