<template>
    <div>
        <select v-model="selected" class="form-select mt-1 block w-full border p-3 rounded" @change="onChange">
            <option value="0">Select Country</option>
            <option :key="i" v-for="(country,i) in countries" :value="country.ID">{{country.Country}}</option>
        </select>
    </div>
</template>

<script>
export default {
    name: 'CountrySelect',
    props: ['countries'],
    data() {
        return {
            selected: 0
        }
    },
    methods: {
        onChange() { 
            // console.log('selected', this.selected) v-model에 바로 담기
            const country = this.countries.find((item) => item.ID === this.selected)
            console.log(country)
            // this.$emit('get-country', )
        }
    },
}
</script>