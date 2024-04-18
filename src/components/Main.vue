<script setup>
import data from '../data.json';
</script>

<template>
    <div class="search">
        <img src="../assets/search.svg" alt="">
        <input @input="search" type="text" name="search" id="search" placeholder="Search for a country…">
    </div>
    <template v-if="myData.length">
        <div class="main__list">
        <RouterLink :to=String(item.name) v-for="item in myData">
            <div class="main__card">
                <img class="main__flag" :src="item.flags.png" alt="">
                <div class="main__info">
                    <h2>{{ item.name }}</h2>
                    <p><strong>Population:</strong> {{ item.population.toLocaleString("en") }}</p>
                    <p><strong>Region:</strong> {{ item.region }}</p>
                    <p><strong>Capital:</strong> {{ item.capital }}</p>

                </div>
            </div>
        </RouterLink>
    </div>
    </template>
    <template v-else>
        <div class="not__found">
            <h2>Нет данных</h2>
        </div>
    </template>
</template>

<script>
// let myData = data
export default {
    data(){
        return {myData: data}
    },
    methods: {
        search(e) {
            let value = e.target.value
            this.myData = data.filter(x => x.name.toLowerCase().startsWith(value.toLowerCase()))
        }
    },
    watch: {

    }
}
</script>