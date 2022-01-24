<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :status="status"/>
    <CountrySelect ref="countrySelect" :countries="countries" @get-country="selectCountry" />

    <button v-if="status.Country" @click="selectGlobal" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600 mb-20">Clear Country</button>

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
      title: '',
      dataDate: '',
      status: '',
      countries: [],
      loadingImage: require('../assets/Spinner-1s-200px.gif'),
      responseData : ''
    }
  },
  async created() {
    await this.fetchCoivdDate()
  },
  methods: {
    async fetchCoivdDate() {
      const data = await
      fetch("https://api.covid19api.com/summary")
      .then(function(res){
        return res.json()
      })
      .then(function(data){
        return data
      });

      this.responseData = data
      this.countries = data.Countries
      this.selectGlobal()
      this.loading = false
    },
    selectCountry(value) {
      if(value === null) { 
        selectGlobal()
        return
      }
      this.title = value.Country
      this.status = value
    },
    selectGlobal() {
      this.dataDate = this.responseData.Date
      this.title = 'Global'
      this.status = this.responseData.Global
      this.$refs.countrySelect.$refs.selected = 0 이거내일해야지
    }
  }
}
</script>
