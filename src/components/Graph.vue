<template>
  <div class="small">
    
    <Dialog
      v-if="ifVisible"
      @closeDialog = "closeDialog"
      @updateData = "updateData"
      v-bind:Aprop="A"
      v-bind:Bprop="B"
      v-bind:Cprop="C"
    />
    <button class="btn btn-primary" @click="showDialog">Chose parameters</button>
    
    <line-chart :chart-data="datacollection" :options="options"></line-chart>
  </div>
</template>

<script>
// Подключение компонента для отображения диаграммы
import LineChart from "../components/LineCharts.js";
import Dialog from '../components/Dialog.vue'

const DATA_COUNT = 50;
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
      A : 2,
      B : 2,
      C : 2,
      ifVisible: false,
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

    
    showDialog() {
      this.ifVisible = true;
    },
    closeDialog() {
      this.ifVisible = false
    },
    updateData(data) {
      this.A = data.aParam
      this.B = data.bParam
      this.C = data.cParam
      this.fillData()
      this.ifVisible = false
    },



    // Функция, которая производит заполнение данных случайным образом
  
    fillData() {
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
      return Math.floor(this.A * Math.pow(x, 3) * Math.sin(this.B * x) - this.C);
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