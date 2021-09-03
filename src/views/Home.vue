<template>
  <main v-if="!loading">
    <!-- Tile /Could be Global or for countries/ -->
    <DataTitle :text="title" :dataDate="dataDate" />

    <!-- Data Boxes -->
    <DataBoxes :stats="stats" />

    <!-- Select Bar -->
    <CountrySelect @get-country="getCountryData" :countries="countries" />

    <!-- Buttom for return to Global data -->
    <div class="flex h-auto justify-center items-center">
      <button
        @click="clearCountryData"
        v-if="stats.Country"
        class="bg-green-700 text-white rounded p-3 mt-10 mb-10 focus:outile-none hover:bg-green-600"
      >
        Clear Country
      </button>
    </div>

    <!-- Chart -->
    <Chart
      v-if="loaded"
      :chartdata="chartData"
      :options="chartOptions"
      :stats="stats"
    />
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-5">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-30 m-auto" alt="" />
  </main>
</template>

<script>
/*-- Import Components --*/
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";
import CountrySelect from "@/components/CountrySelect";
import Chart from "../components/Chart";

/*-- Import Dev Dependencies --*/
import moment from "moment";

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
    Chart,
  },
  data() {
    return {
      loading: true,
      loaded: false,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/loading.gif"),
      chartData: [],
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = "Global";
      this.stats = data.Global;
      this.loading = false;
    },
  },
  /*-- Life Cycle Methods --*/
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
  async mounted() {
    this.loaded = false;
    try {
      this.loaded = true;
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
