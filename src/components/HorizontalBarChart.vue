<template>
  <div class="small">
    <horizontal-bar-chart
      :chart-data="datacollection"
      :options="chartOptions"
    ></horizontal-bar-chart>
  </div>
</template>

<script>
// TODO UPDATE CHART LABELS AND REORDER
import { mapState, mapGetters } from "vuex";
import HorizontalBarChart from "./HorizontalBarChart.js";

export default {
  components: {
    HorizontalBarChart,
  },
  data: function() {
    return {
      datacollection: {},
      fieldAliases: {},
      chartOptions: {
        legend: {
          display: false,
        },
        scales: {
          xAxes: [
            {
              ticks: {
                beginAtZero: true,
              },
            },
          ],
        },
      },
    };
  },
  mounted() {},
  created() {
    /* 
     also can be:
    created: function() {
  }, 
  */
  },
  methods: {
    fillData() {
      this.datacollection = {
        labels: this.getSummaryStats.map(obj => obj.key),
        datasets: [
          {
            label: `data`,
            backgroundColor: `#f87979`,
            data: this.getSummaryStats.map(obj => obj.value),
          },
        ],
      };
    },
    getRandomInt() {
      return Math.floor(Math.random() * (50 - 5 + 1)) + 5;
    },
  },
  computed: {
    ...mapState([`mapViewData`]),
    ...mapGetters([`getSummaryStats`]),
  },
  watch: {
    getSummaryStats: function() {
      this.fillData();
    },
  },
};
</script>

<style>
.small {
  max-width: 600px;
  margin: 150px auto;
}
</style>