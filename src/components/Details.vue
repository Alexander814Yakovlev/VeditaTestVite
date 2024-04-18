<script setup>
import { RouterLink } from 'vue-router';
import data from '../data.json';
</script>
<template>
    <RouterLink class="details__return" to="/"><img src="../assets/back.svg" alt=""> Back</RouterLink>
    <div>
        <div class="detail__card">
            <img class="detail__flag" :src="country.flags.png" alt="">
            <div class="detail__info">
                <h2>{{ country.name }} </h2>
                <div class="details__info_inner">
                    <div class="details__widescreen_1">
                    <p><strong>Native name:</strong> {{ country.nativeName }}</p>
                    <p><strong>Population:</strong> {{ country.population.toLocaleString("en") }}</p>
                    <p><strong>Region:</strong> {{ country.region }}</p>
                    <p><strong>Sub Region:</strong> {{ country.subregion }}</p>
                    <p><strong>Capital:</strong> {{ country.capital }}</p>
                </div>

                <div class="details__widescreen_2">
                    <p><strong>Top Level Domain:</strong> {{ country.topLevelDomain.join(", ") }}</p>
                    <!-- Not all countries has currencies -->
                    <p v-if="country.currencies"><strong>Currencies:</strong> {{ country.currencies.map(x => x.name).join(", ") }}</p>
                    <p><strong>Languages:</strong> {{ country.languages.map(x => x.name).join(", ") }}</p>
                </div>
                </div>
                
                <!-- Not all countries has land borders -->
                <div class="details__borders_wrapper" v-if="country.borders">
                    <div class="details__borders_title">
                        <p><strong>Border Countries: </strong></p>
                    </div>
                    
                    <div class="details__borders">
                        <RouterLink v-for="item of borders" :to=item class="details__borders_item">
                            {{ item }}
                        </RouterLink>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
<script>
export default {
    data() {
        return {
            name: this.$route.params['name'],
        }
    },
    computed: {
        country() {
            return data.filter(x => x.name == this.$route.params['name'])[0]
        },
        borders() {
            let countries = []
            for (let item of data) {
                if (data.filter(x => x.name == this.$route.params['name'])[0].borders.includes(item.alpha3Code)) {
                    countries.push(item.name)
                }
            }
            return countries
        }
    }
}
</script>