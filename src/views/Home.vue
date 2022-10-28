<template>
  <div class="home">
    <main>
      <DataTitle :text="title" :dataDate="dataDate" />
      <DataBoxes :stats="stats" />

      <CountrySelect @get-country="getCountryData" :countries="countries" />
    </main>
  </div>
</template>

<script>
import CountrySelect from '@/components/CountrySelect';
import DataBoxes from '@/components/DataBoxes';
import DataTitle from '@/components/DataTitle';
import { ref } from 'vue';

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },

  setup() {
    const loading = ref(true);
    const title = ref('Global');
    const dataDate = ref('');
    const stats = ref({});
    const countries = ref([]);

    const fetchCovidData = async () => {
      const res = await fetch('https://api.covid19api.com/summary');
      return await res.json();
    };

    const getCountryData = (country) => {
      stats.value = country;
      title.value = country.Country;
    };

    const baseSetup = async () => {
      const data = await fetchCovidData();
      dataDate.value = data.Date;
      stats.value = data.Global;
      countries.value = data.Countries;
      loading.value = false;
    };

    baseSetup();

    return {
      loading,
      title,
      dataDate,
      stats,
      countries,
      getCountryData
    };
  }
};
</script>