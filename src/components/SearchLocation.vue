<template>
    <form @submit.prevent="submitCity">
        <div class="search-container">
            <span class="material-icons search"> search </span>
            <input class="search-box" placeholder="search city" type="text" v-model="city" />
        </div>
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
    justify-content: space-between;
    margin: auto 13px;
}

.search-container {
    position: relative;
    display: flex;
    align-items: center;
}

.search-box {
    width: 252px;
    height: 48px;
    box-sizing: border-box;
    border: solid 1px var(--off-white);
    border-radius: 0;
    background-color: var(--blue);
    font-size: 16px;
    font-weight: 500;
    text-indent: 49px;
    color: var(--darker-grey);
    margin-right: 12px;
}

.search-box:focus {
    outline: none;
    border: solid 1px var(--off-white);
}

.search {
    position: absolute;
    width: 17px;
    left: 17px;
    color: var(--darker-grey);
}

.submit-button {
    all: unset;
    box-sizing: border-box;
    border: solid 1px var(--sky-blue);
    background-color: var(--sky-blue);
    height: 48px;
    width: 86px;
    text-align: center;
    font-size: 16px;
    font-weight: 600;
}

.submit-button:hover {
    cursor: pointer;
}

@media (min-width: 768px) {
    form {
        flex-direction: column;
        align-items: center;
        gap: 20px;
    }
}

@media (min-width: 992px) {
    form {
        flex-direction: row;
    }
    .search-box {
        width: 268px;
    }
}
</style>
