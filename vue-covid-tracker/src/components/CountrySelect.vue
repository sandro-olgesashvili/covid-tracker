<template>
   <select v-model="selected" class="form-select mt-10 w-full p-3 rounded border block" @change="onChange()">
       <option value="0">Select Country</option>
       <option v-for="country in countries" :value="country.ID" :key="country.ID">{{country.Country}}</option>
   </select>
</template>

<script>
export default {
    name:'CountrySelect',
    props:['countries'],
    data() {
        return {
            selected: 0,
        }
    },

    methods: {
        onChange() {
            const country = this.countries.find((item) => {
                return item.ID === this.selected
            });

            console.log(country)

            this.$emit('get-country', country)
        }
    }
}
</script>

<style>

</style>