<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :status="status"/>
    <CountrySelect :countries="countries" />
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
    }
  }
}
</script>
