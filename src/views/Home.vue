<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :status="status"/>
    <CountrySelect :countries="countries" @get-country="testCountry" />

    <button v-if="status.Country" @click="clearCountryData" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600 mb-20">Clear Country</button>

  </main>
  <main calss="flex flex-col allign-center justify=center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="">
  </main>

</template>

<script>
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'
import CountrySelect from '@/components/CountrySelect'
export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      status: '',
      countries: [],
      loadingImage: require('../assets/Spinner-1s-200px.gif')
    }
  },
  async created() {
    const data = await this.fetchCoivdDate()
    console.log(data)
    this.dataDate = data.Date
    this.status = data.Global
    this.countries = data.Countries
    this.loading = false
  },
  methods: {
    async fetchCoivdDate() {
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    },
    testCountry(value) {
      this.status = value
      this.title = value.Country
    },
    async clearCountryData() {
      this.loading = true
      const data = await this.fetchCoivdDate()
      this.title = 'Global'
      this.status = data.Global
      this.loading = false
    }
  }
}
</script>
