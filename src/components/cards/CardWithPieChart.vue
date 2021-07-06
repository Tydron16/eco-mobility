<template>
  <div class="col-lg-6 col-md-6 col-sm-12 col-xs-12">
    <q-card class="my-card">
      <IEcharts style="height: 450px" :option="PieChart" :resizable="true" />
    </q-card>
  </div>
</template>

<script>
import IEcharts from "vue-echarts-v3/src/full.js";

export default {
  name: "CardWithPieChart",

  components: {
    IEcharts
  },

  data() {
    return {
      PieChart: {
        tooltip: {
          trigger: "item"
        },
        legend: {
          top: "5%",
          left: "center"
        },
        color: [
          "#5470c6",
          "#91cc75",
          "#fac858",
          "#ee6666",
          "#73c0de",
          "#3ba272",
          "#fc8452",
          "#9a60b4",
          "#ea7ccc"
        ],
        series: [
          {
            name: "Veicoli",
            type: "pie",
            radius: ["40%", "70%"],
            avoidLabelOverlap: false,
            itemStyle: {
              borderRadius: 10,
              borderColor: "#fff",
              borderWidth: 2
            },
            label: {
              show: false,
              position: "center"
            },
            emphasis: {
              label: {
                show: true,
                fontSize: "40",
                fontWeight: "bold"
              }
            },
            labelLine: {
              show: false
            },
            data: [
              { value: 1048, name: "Motorino" },
              { value: 735, name: "Auto" },
              { value: 580, name: "Bicicletta" },
              { value: 484, name: "EV" },
              { value: 300, name: "E-Bike" }
            ]
          }
        ]
      }
    };
  }
};
</script>
