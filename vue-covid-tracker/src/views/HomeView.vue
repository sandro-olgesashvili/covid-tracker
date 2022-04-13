<template>
  <main v-if="!loading">

  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>

    <img :src="loadingImage" class="w-24 m-auto" alt="">
    
  </main>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: {
    
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
    }
  },


  async created() {
    const data = await this.fetchCovidDate();
    
    console.log(data)


    this.dataDate = data.Date
    this.countries = data.Countries
    this.stats = data.Global
    this.loading= false

  }
}
</script>
