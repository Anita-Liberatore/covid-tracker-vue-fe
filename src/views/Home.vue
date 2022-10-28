<template>
  <div class="home">
    <main>
        <DataTitle :text="title" :dataDate="dataDate"/>
        <DataBoxes :stats="stats"/>

        <CountrySelect @get-country="getCountryData" :countries="countries"/>

    </main>
  </div>
</template>

<script>
import DataTitle from '@/components/DataTitle.vue'
import DataBoxes from '@/components/DataBoxes.vue'
import CountrySelect from '@/components/CountrySelect.vue'



export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data() {
    return {
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary');
      return await res.json();
    },

    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
  },
};
</script>
