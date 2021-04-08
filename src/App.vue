<template>
  <div class="app">
    <div class="label"><h1 class="head">Pie Chart</h1></div>
    <div class="charts">
      <div class="pie-chart">
        <pie-chart
          :colors="colors"
          :data="genderData"
          :legend="false"
          width="300px"
          height="300px"
        ></pie-chart>
        <div class="label"><h2>by Gender</h2></div>
      </div>
      <div class="pie-chart">
        <pie-chart
          :donut="true"
          :colors="colors"
          :data="countryData"
          :legend="false"
          width="300px"
          height="300px"
        ></pie-chart>
        <div class="label"><h2>by Country</h2></div>
      </div>
    </div>
    <div>
      <div class="label"><h1 class="head">Table Data</h1></div>
      <Table v-bind:data="csvData" />
    </div>
  </div>
</template>

<script>
import csvFile from "./MOCK_DATA.csv";
import Table from "./components/Table";

export default {
  name: "App",
  components: { Table },

  data: function () {
    return {
      genderData: [],
      countryData: [],
      csvData: [],
      colors: [],
    };
  },

  methods: {
    sortGenderData(data) {
      if (data.length < 1) throw "no csv data was found";
      const genderData = {};
      data.forEach((item) => {
        if (item.gender === undefined) {
          console.log(item);
        }
        if (genderData[item.gender] === undefined) genderData[item.gender] = 1;
        else genderData[item.gender] += 1;
      });
      return genderData;
    },

    sortCountryData(data) {
      if (data.length < 1) throw "no csv data was found";
      const countryData = {};
      data.forEach((item) => {
        if (countryData[item.country] === undefined)
          countryData[item.country] = 1;
        else countryData[item.country] += 1;
      });
      return countryData;
    },

    // Exracting color to use in pie chart
    extractColors(data) {
      return data.map((item) => {
        return item.favourite_color;
      });
    },
  },

  mounted() {
    // Extracting respective data from CSV file for the pie chart
    const sortedGenders = this.sortGenderData(csvFile);
    const sortedCountries = this.sortCountryData(csvFile);

    // Populate all the data
    this.genderData = sortedGenders;
    this.countryData = sortedCountries;
    this.csvData = csvFile;
    this.colors = this.extractColors(csvFile);
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: Arial, Helvetica, sans-serif;
}
.app {
  width: 70vw;
  margin: 0 auto;
}

.charts {
  padding: 2rem;
  display: flex;
  width: 100%;
  justify-content: space-evenly;
}
.label {
  width: 100%;
  text-align: center;
  padding: 1rem;
  color: rgb(97, 97, 97);
}
.head {
  color: rgb(44, 44, 44);
}
</style>
