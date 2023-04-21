<template>
  <div>
    <div class="card" style="width: 18rem" v-if="detail != null">
      <img
        :src="detail?.flags?.png"
        class="card-img-top"
        :alt="detail?.flags?.alt"
      />
      <div class="card-body">
        <h5 class="card-title">
          {{ detail?.name?.common }} ({{ detail?.name?.official }})
        </h5>
        <h5 class="card-title" v-if="detail?.region">
          {{ detail?.region }} ({{ detail?.subregion }})
        </h5>
        <p class="card-text">{{ detail?.flags?.alt }}</p>
        <p class="card-text">
          Population : {{ detail.population.toLocaleString() }}
        </p>
        <p class="card-text">Capital : {{ detail.capital.join(', ') }}</p>
        <span class="badge bg-primary" v-if="detail.unMember"
          >Member of United Nations</span
        >
        <a :href="detail.maps.googleMaps" class="card-link">googleMaps</a>
        <a :href="detail.maps.openStreetMaps" class="card-link"
          >openStreetMaps</a
        >
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    props: ['country'],
    data: () => ({
      detail: null,
    }),
    watch: {
      country(newValue) {
        this.getCountryDetail(newValue)
      },
    },
    methods: {
      getCountryDetail(country) {
        axios
          .get('https://restcountries.com/v3.1/name/' + country)
          .then((response) => {
            this.detail = response.data[0]
          })
          .catch(function (error) {
            console.log(error)
          })
      },
    },
  }
</script>
