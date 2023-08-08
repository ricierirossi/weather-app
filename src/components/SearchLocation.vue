<template>
    <form @submit.prevent="submitCity">
        <span class="material-icons search"> search </span>
        <input class="search-box" placeholder="search city" type="text" v-model="city" />
        <input class="submit-button" type="submit" value="Search" />
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
form {
    display: flex;
    /* justify-content: center; */
    margin-top: 38px;
    height: 48px;
    width: 459px;
}
.search-box {
    width: 262px;
    margin-left: 47px;
    border: solid 1px #616475;
    border-radius: 0;
    background-color: #1e213a;
    color: #616475;
    text-indent: 49px;
}

.search-box:focus {
    outline: none;
    border: solid 1px #e7e7eb;
}

.search {
    position: absolute;
    height: 17px;
    width: 17px;
    left: 62px;
    top: 97px;
    color: #616475;
}

.submit-button {
    all: unset;
    width: 86px;
    border: solid 1px #3c47e9;
    background-color: #3c47e9;
    text-align: center;
    font-size: 16px;
    margin-left: 12px;
}

.submit-button:hover {
    cursor: pointer;
}
</style>
