<template>
  <main v-if="!loading">
    <DataTitle :text='title' :dataDate="dataDate"/>
    <DataBoxes :stats='stats'/>
    <CountrySelect @get-country='getCountryData' :countries='countries' />

    <button @click="clearCountryData" v-if="stats.Country" class="bg-green-700 text-white p-3 mt-10 focus:outline-none hover:bg-green 600 rounded">Clear Country</button>
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center flex justify-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>

    <img :src="loadingImage" class="w-24 m-auto" alt="">
    
  </main>
</template>

<script>
// @ is an alias to /src
import DataTitle from '../components/DateTitle.vue'
import DataBoxes from '../components/DataBoxes.vue'
import CountrySelect from '../components/CountrySelect.vue'

export default {
  name: 'HomeView',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },

  data() {
    return {
      loading:true,
      title:'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')

    }
  },


  methods:{
    async fetchCovidDate() {
      const res =  await fetch('https://api.covid19api.com/summary');
      const data = await res.json ();
      return data
    },

    getCountryData(country) {
      this.title= country.Country;
      this.stats = country;

    },

    async clearCountryData () {
      this.loading = true
      const data = await this.fetchCovidDate();

      this.stats = data.Global

      this.title= 'Global';

      this.loading = false
    }

  },


  async created() {
    const data = await this.fetchCovidDate();
    
    console.log(data)
    console.log(data.Global.Country)

    this.dataDate = data.Date
    this.countries = data.Countries
    this.stats = data.Global
    this.loading= false

  }
}
</script>
