<template>
    <div>
        <select v-model="selected" class="form-select mt-1 block w-full border p-3 rounded">
            <option value="0">Select Country</option>
            <option :key="i" v-for="(country,i) in countries" :value="country.ID"></option>
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
    }
}
</script>