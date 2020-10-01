<template lang="html">
  <div>
    <h1 class="cyan--text display-4 font-weight-light">
      Picture of the Day
    </h1>
    <h4 class="font-weight-light">
      Date must be between 16 Jun 1995 and 1 Oct 2020
    </h4>
    <div style="max-width:20%">
      <v-text-field v-model="DayID" type="text" label="Day [INT ONLY]" />
      <v-text-field v-model="MonthID" type="text" label="Month [INT ONLY]" />
      <v-text-field v-model="YearID" type="text" label="Year [INT ONLY]" />
      <v-btn color="primary" @click="Search">
        Search
      </v-btn>
      </v-date-picker>
    </div>
    <v-divider class="mt-2 mb-2" />
    <div v-for="list in ID" :key="list.date">
      <!-- {{list}} -->
      <nuxt-link :to=" {name: 'product-id', params: { id: list }} ">
        <img
          style="max-width:60%"
          :src="list.hdurl"
        >
      </nuxt-link>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      ID: null,
      YearID: '',
      MonthID: '',
      DayID: '',
      DateID: ''
    }
  },
  methods: {
    Search () {
      const url = 'https://api.nasa.gov/planetary/apod?date=' + this.YearID + '-' + this.MonthID + '-' + this.DayID + '&hd=true&api_key=iK6QWVlZ9w0RUsSNWob3UL5KcXFehRlXBHvKuW6p'
      axios.get(url).then((response) => {
        this.ID = response
      })
    }
  }
}
</script>
<style lang="css" scoped></style>
