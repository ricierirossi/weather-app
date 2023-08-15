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
    justify-content: space-around;
    width: 100vw;
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
        width: 100%;
        gap: 12px;
    }

    .search-box {
        width: 100%;
    }

    .submit-button {
        min-width: 86px;
    }
}

@media (min-width: 992px) {
    .search-box {
        width: 268px;
    }
}
</style>

<!-- <style scoped>
form {
    display: flex;
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

@media (max-width: 375px) {
    form {
        margin-top: 38px;
        width: 375px;
    }
    .search-box {
        width: 246px;
        margin-left: 13px;
    }

    .search {
        left: 28px;
    }
}
</style> -->
