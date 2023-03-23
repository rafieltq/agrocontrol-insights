<template>
  <q-page padding>
    <q-card class="q-pa-md">
      <div class="row items-center">
        <div :class="$q.screen.md ? 'col-md-2 q-mx-xs' : 'col-xs-12 q-mb-md'">
          <measure-card
            title="pH"
            value="7.0"
            text="text-white"
            styles="background: radial-gradient(circle, #898121 0%, #539165 100%)"
            bordered
            flat
          />
        </div>
        <div :class="$q.screen.md ? 'col-md-2 q-mx-xs' : 'col-xs-12 q-mb-md'">
          <measure-card
            title="Temperature"
            value="25.0"
            text="text-white"
            styles="background: radial-gradient(circle, #35a2ff 0%, #014a88 100%)"
            bordered
            flat
          />
        </div>
        <div :class="$q.screen.md ? 'col-md-2 q-mx-xs' : 'col-xs-12 q-mb-md'">
          <measure-card
            title="Soil Moisture"
            value="25.0"
            text="text-white"
            styles="background: radial-gradient(circle, #FF7B54 0%, #C27664 100%);"
            bordered
            flat
          />
        </div>
      </div>
    </q-card>
    <q-card class="q-mt-md q-pa-md">
      <div class="row">
        <div class="col-md-6 col-xs-12">
          <apexchart
            width="500"
            type="line"
            :options="options"
            :series="series"
            :title="title"
          ></apexchart>
        </div>

        <div class="col-md-6 col-xs-12">
          <apexchart
            width="500"
            type="line"
            :options="options_electroconductivity"
            :series="series_electroconductivity"
            :title="title"
          ></apexchart>
        </div>
      </div>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
import MeasureCard from "../components/Measures/MeasureCard.vue";

const options = ref({
  chart: {
    height: 350,
    type: "line",
    dropShadow: {
      enabled: true,
      color: "#000",
      top: 18,
      left: 7,
      blur: 10,
      opacity: 0.2,
    },
    toolbar: {
      show: false,
    },
  },
  colors: ["#77B6EA", "#545454"],
  dataLabels: {
    enabled: true,
  },
  stroke: {
    curve: "smooth",
  },
  title: {
    text: "Average High & Low Temperature",
    align: "left",
  },
  grid: {
    borderColor: "#e7e7e7",
    row: {
      colors: ["#f3f3f3", "transparent"], // takes an array which will be repeated on columns
      opacity: 0.5,
    },
  },
  markers: {
    size: 1,
  },
  xaxis: {
    categories: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul"],
    title: {
      text: "Month",
    },
  },
  yaxis: {
    title: {
      text: "Temperature",
    },
    min: 5,
    max: 40,
  },
  legend: {
    position: "top",
    horizontalAlign: "right",
    floating: true,
    offsetY: -25,
    offsetX: -5,
  },
});

const series = ref([
  {
    name: "High - 2013",
    data: [28, 29, 33, 36, 32, 32, 33],
  },
  {
    name: "Low - 2013",
    data: [12, 11, 14, 18, 17, 13, 13],
  },
]);

const options_electroconductivity = ref({
  chart: {
    height: 350,
    type: "line",
    dropShadow: {
      enabled: true,
      color: "#000",
      top: 18,
      left: 7,
      blur: 10,
      opacity: 0.2,
    },
    toolbar: {
      show: false,
    },
  },
  colors: ["#EBB02D", "#545454"],
  dataLabels: {
    enabled: true,
  },
  stroke: {
    curve: "smooth",
  },
  title: {
    text: "Average High & Low Soil electroconductivity",
    align: "left",
  },
  grid: {
    borderColor: "#e7e7e7",
    row: {
      colors: ["#f3f3f3", "transparent"], // takes an array which will be repeated on columns
      opacity: 0.5,
    },
  },
  markers: {
    size: 1,
  },
  xaxis: {
    categories: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul"],
    title: {
      text: "Month",
    },
  },
  yaxis: {
    title: {
      text: "Electroconductivity",
    },
    min: 5,
    max: 40,
  },
  legend: {
    position: "top",
    horizontalAlign: "right",
    floating: true,
    offsetY: -25,
    offsetX: -5,
  },
});

const series_electroconductivity = ref([
  {
    name: "High - 2013",
    data: [28, 29, 33, 36, 32, 32, 33],
  },
  {
    name: "Low - 2013",
    data: [12, 11, 14, 18, 17, 13, 13],
  },
]);
</script>

<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 250px
</style>
