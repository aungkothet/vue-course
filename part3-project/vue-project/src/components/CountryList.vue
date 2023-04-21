<script>
  import axios from 'axios'
  import CountryCard from './CountryCard.vue'
  export default {
    components: {
      CountryCard
    },
    methods: {
      getCountries() {
        axios
          .get('https://restcountries.com/v3.1/all?fields=name,flags')
          .then((response) => {
            console.log(response.data)
            this.countryList = response.data
          })
          .catch(function (error) {
            console.log(error)
          })
      },
    },
    data: () => ({
      countryList: [],
      selectedCountry: "",
    }),
    mounted() {
      this.getCountries()
    },
  }
</script>

<template>
  <div class="row">
    <div class="mb-3">
      <label class="form-label"
        >Country - Total Count = {{ countryList.length }}</label
      >
      <select
        class="form-select"
        aria-label="Default select example"
        v-model="selectedCountry"
      >
        <option v-for="(country, key) in countryList" :value="country?.name?.common" :key="key">
          {{ country?.name?.common }} ({{ country?.name?.official }})
        </option>
      </select>
    </div>
    <CountryCard
      :country="selectedCountry"
      v-if="selectedCountry"
    ></CountryCard>
  </div>
</template>
