<template>
  <div class="grid md:grid-cols-2 gap-4">
      <div class="shadow-md bg-blue-100 p-10 text-center rounded">
          <h3 class="text-blue-900 font-bold mb-4 text-3xl">Cases</h3>
          <div class="text-2xl mb-4">
              <span class="font-bold">New:</span>
              {{numbersWithCommas(stats.NewConfirmed)}}
          </div>
          <div class="text-2xl mb-4">
              <span class="font-bold">total:</span>
              {{numbersWithCommas( stats.TotalConfirmed)}}
          </div>
      </div>

      <div class="shadow-md bg-blue-200 p-10 text-center rounded">
          <h3 class="text-blue-900 font-bold mb-4 text-3xl">Deaths</h3>
          <div class="text-2xl mb-4">
              <span class="font-bold">New:</span>
              {{numbersWithCommas(stats.NewDeaths)}}
          </div>
          <div class="text-2xl mb-4">
              <span class="font-bold">total:</span>
              {{numbersWithCommas(stats.TotalDeaths)}}
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'DataBoxes',
    props:['stats'],

    methods: {
        numbersWithCommas(x) {
            return  x.toString()
          .replace(/\B(?=(\d{3})+(?!\d))/g, ',');
        }
    }


}
</script>

<style>

</style>