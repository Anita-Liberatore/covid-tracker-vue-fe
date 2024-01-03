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

    /*const fetchCovidData = async () => {
      const res = await fetch('https://api.covid19api.com/summary');
      return await res.json();
    }; */

    const getCountryData = (country) => {

      if(country === 'Italy') {
        stats.value = {
          'NewConfirmed': 148,
          'TotalConfirmed': 437,
          'NewDeaths': 34,
          'TotalDeaths': 329
        };

        title.value = country;
      } else if(country === 'England') {
        stats.value = {
          'NewConfirmed': 14867,
          'TotalConfirmed': 43743,
          'NewDeaths': 3,
          'TotalDeaths': 450
        };

        title.value = country;
      } else {
        stats.value = {
          'NewConfirmed': 1483,
          'TotalConfirmed': 43,
          'NewDeaths': 343,
          'TotalDeaths': 3299
        };

        title.value = country;
      }

    };

    const baseSetup = async () => {
      //const data = await fetchCovidData();
      dataDate.value = new Date();
      stats.value = {
        'NewConfirmed': 148483829,
        'TotalConfirmed': 43727828,
        'NewDeaths': 3438229,
        'TotalDeaths': 32929402
      };
      countries.value = ['Italy', 'Germany', 'England'];
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