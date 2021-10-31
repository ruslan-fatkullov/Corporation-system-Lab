<template>
  <div class="small">
    <Dialog/>
    <div class="our-b btn btn-primary" type="submit" @click="fillData">Randomize</div>
    <line-chart :chart-data="datacollection" :options="options"></line-chart>
  </div>
</template>

<script>
// Подключение компонента для отображения диаграммы
import LineChart from "../components/LineCharts.js";
import Dialog from "../components/Dialog.vue";

const DATA_COUNT = 50;
var A = Math.random() * 5;
var B = 3;
var C = 0;
var labels = [];
for (let i = -25; i <= DATA_COUNT / 2 + 1; ++i) {
  labels.push(i.toString());
}

export default {
  // Описание используемых в шаблоне компонентов
  components: {
    LineChart,
    Dialog
  },
  data() {
    return {
      // Данные для диаграммы
      datacollection: null,
      // Настройка параметров диаграммы
      options: null,
    };
  },
  // Заполнение this.datacollection и this.options начальными статическими значениями
  created() {
    this.datacollection = {};
    this.options = {
      responsive: true,
      title: {
        display: true,
        text: "Line Chart",
      },
      tooltips: {
        mode: "index",
        intersect: false,
      },
      hover: {
        mode: "nearest",
        intersect: true,
      },
      scales: {
        xAxes: [
          {
            display: true,
            scaleLabel: {
              display: true,
              labelString: "X values",
            },
          },
        ],
        yAxes: [
          {
            display: true,
            scaleLabel: {
              display: true,
              labelString: " Y Value",
            },
          },
        ],
      },
    };
  },
  mounted() {
    // Заполнение данных с помощью функции fillData
    this.fillData();
  },
  methods: {
    // Функция, которая производит заполнение данных случайным образом
    fillData() {
      A = Math.random() * 10;  
      B = Math.random() * 10;  
      C = Math.random() * 999;  
      this.datacollection = {
        labels: labels,
        datasets: [
          {
            label: "My First dataset",
            backgroundColor: "#F00",
            borderColor: "#F00",
            data: this.fillMassive(),
            fill: false,
          },
        ],
      };
    },
    randomScalingFactor(x) {
      return Math.floor(A * Math.pow(x, 3) * Math.sin(B * x) - C);
    },
    fillMassive() {
      var data = [];
      for (let i = 0; i < DATA_COUNT + 1; ++i) {
        data.push(this.randomScalingFactor(labels[i]));
      }
      return data
    },
  },
};
</script>
<style scoped>
.small {
  max-width: 600px;
  margin: 100px auto;
}
.our-b{
  margin-left: 40%;
}
</style>