<template>
  <q-page padding>
    <q-card class="q-pa-md">
      <div class="row">
        <div :class="$q.screen.xs ? 'col-xs-12 q-mb-md' : 'col-md-4 q-mx-xs'">
          <measure-card
            title="pH"
            :value="pH"
            text="text-white"
            styles="background: radial-gradient(circle, #898121 0%, #539165 100%);"
            bordered
            flat
          />
        </div>
        <div :class="$q.screen.xs ? 'col-xs-12 q-mb-md' : 'col-md-4 q-mx-xs'">
          <measure-card
            title="Temperatura °C"
            :value="temperature"
            text="text-white"
            styles="background: radial-gradient(circle, #35a2ff
          0%, #014a88 100%)"
            bordered
            flat
          />
        </div>
        <div :class="$q.screen.xs ? 'col-xs-12 q-mb-md' : 'col-md-3 q-mx-xs'">
          <measure-card
            title="Humedad del suelo"
            :value="seriesMoisture[4]"
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
        <q-card bordered class="col-md-5 col-xs-12">
          <apexchart
            width="500"
            type="line"
            :options="options"
            :series="series"
            :title="options.title"
          ></apexchart>
        </q-card>

        <div class="col-1"></div>

        <q-card bordered class="col-md-6 col-xs-12">
          <apexchart
            width="500"
            type="line"
            :options="options_electroconductivity"
            :series="series_electroconductivity"
            :title="title"
          ></apexchart>
        </q-card>
      </div>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, onMounted, reactive } from "vue";
import MeasureCard from "../components/Measures/MeasureCard.vue";

const options = ref({
  title: {
    text: "Humedad del suelo",
    align: "center",
  },
  chart: {
    grid: {
      borderColor: "#e7e7e7",
      row: {
        colors: ["#f3f3f3", "transparent"], // takes an array which will be repeated on columns
        opacity: 0.5,
      },
    },
    id: "realtime",
    height: 350,
    type: "line",
    animations: {
      enabled: true,
      easing: "linear",
      dynamicAnimation: {
        speed: 1000,
      },
    },
    toolbar: {
      show: false,
    },
    dropShadow: {
      enabled: true,
      color: "#000",
      top: 18,
      left: 7,
      blur: 10,
      opacity: 0.2,
    },
    // https://apexcharts.com/docs/options/chart/animations/
    animations: {
      enabled: true,
      easing: "linear",
      speed: 200,
      animateGradually: {
        enabled: false,
      },

      dynamicAnimation: {
        enabled: true,
        speed: 150,
      },
    },
    yaxis: {
      max: 15,
    },
  },
  dataLabels: {
    enabled: true,
  },
  stroke: {
    curve: "smooth",
  },
  markers: {
    size: 2,
  },
  colors: ["#9c652e", "#279d00"],
  zoom: {
    enabled: false,
  },
});

const seriesMoisture = reactive([14.22, 14.27, 14.28, 14.33, 14.44]);

const series = reactive([
  {
    name: "Moisture",
    data: seriesMoisture,
  },
]);

const updateChart = () => {
  const max = 14.99;
  const min = 14;
  // make number oscil between 14 and 14.99
  const newData = series[0].data.map(() => {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  });

  seriesMoisture.push(newData[4]);
  seriesMoisture.shift();
};

onMounted(() => {
  setInterval(updateChart, 1000);
  setInterval(temperatureRandom, 3600);
  setInterval(pHRandom, 3000);
});

const temperature = ref(26);

// generate random numbers for temperature card data just return a random number between 29 and 32
const temperatureRandom = () => {
  const random = () => {
    return Math.floor(Math.random() * (32 - 29 + 1)) + 29;
  };

  temperature.value = random();
};

const pH = ref(7.0);

// generate random numbers for temperature card data just return a random number
const pHRandom = () => {
  const random = () => {
    return Math.floor(Math.random() * (7 - 6 + 1)) + 5;
  };

  pH.value = random();
};

const options_electroconductivity = ref({
  title: {
    text: "Electroconductividad",
    align: "center",
  },
  chart: {
    id: "realtime",
    height: 350,
    type: "line",
    animations: {
      enabled: true,
      easing: "linear",
      dynamicAnimation: {
        speed: 1000,
      },
    },
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
    zoom: {
      enabled: false,
    },
  },
  stroke: {
    curve: "smooth",
  },
  dataLabels: {
    enabled: true,
  },
  colors: ["#EBB02D"],
  // https://apexcharts.com/docs/options/chart/animations/
  animations: {
    enabled: true,
    easing: "linear",
    speed: 200,
    animateGradually: {
      enabled: false,
    },

    dataLabels: {
      enabled: false,
    },
    dynamicAnimation: {
      enabled: true,
      speed: 150,
    },
    yaxis: {
      max: 15,
    },
    markers: {
      size: 1,
    },
  },
});

const seriesElectroconductivity = reactive([22, 22, 20, 21, 22]);

const series_electroconductivity = reactive([
  {
    name: "Electroconductivity",
    data: seriesElectroconductivity,
  },
]);
</script>

<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 250px
</style>
