template>
<template>
  <div class="home">
    <main v-if="!loading" class="home">Show data</main>

    <main class="flex flex-col align-center justify-center text-center" v-else>
        <div class="text-gray-500 text-3xl mt-10 mb-6">
            Fetching Data
        </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "Home",
  components: {},
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      status: {},
      countries: [],
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
  },
  async created() {
    const data = this.fetchCovidData();
    this.dataDate = data.dataDate;
    this.stats = data.Global;
    this.countries = data.Contries;
  },
};
</script>
