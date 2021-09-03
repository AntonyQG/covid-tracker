<template>
  <div class="w-400 h-400">
    <div class="text-2xl mb-4"></div>
    <canvas id="confirmedChart"></canvas>
    <canvas id="deathsChart"></canvas>
  </div>
</template>

<script>
import Chart from "chart.js";

export default {
  name: "Chart",
  props: ["stats"],
  data() {
    return {
      loaded: true,
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },

  /*-- Life Cycle Methods --*/

  async mounted() {
    this.loaded = true;
    var ctx = document.getElementById("confirmedChart");
    var ctxDesths = document.getElementById("deathsChart");
    /*-- Chart of New Cases --*/
    var myChart = new Chart(ctx, {
      type: "bar",
      data: {
        labels: ["New Confirmed", "New Deaths"],
        datasets: [
          {
            label: "New",
            data: [this.stats.NewConfirmed, this.stats.NewDeaths],
            fill: true,
            backgroundColor: "rgba(54, 162, 235, 0.2)",
            borderColor: "rgb(54, 162, 235)",
            tension: 0.1,
            borderWidth: 1,
            hoverBackgroundColor: "rgb(54, 192, 235)",
          },
        ],
      },
      options: {
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      },
    });
    /*-- Chart of Deaths Cases --*/
    var myChartDeaths = new Chart(ctxDesths, {
      type: "bar",
      data: {
        labels: ["Total Confirmed", "Total Deaths"],
        datasets: [
          {
            label: "Total",
            data: [this.stats.TotalConfirmed, this.stats.TotalDeaths],
            fill: true,
            backgroundColor: "rgba(255, 99, 132, 0.2)",
            borderColor: "rgb(255, 99, 132)",
            tension: 0.1,
            borderWidth: 1,
            hoverBackgroundColor: "rgb(230, 56, 56)",
          },
        ],
      },
      options: {
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      },
    });
    console.log(myChart);
    console.log(myChartDeaths);
  },

  async updated() {
    this.loaded = true;
    var ctx = document.getElementById("confirmedChart");
    var ctxDesths = document.getElementById("deathsChart");
    /*-- Chart of New Cases --*/
    var myChart = new Chart(ctx, {
      type: "bar",
      data: {
        labels: ["New Confirmed", "New Deaths"],
        datasets: [
          {
            label: "New",
            data: [this.stats.NewConfirmed, this.stats.NewDeaths],
            fill: true,
            backgroundColor: "rgba(54, 162, 235, 0.2)",
            borderColor: "rgb(54, 162, 235)",
            tension: 0.1,
            borderWidth: 1,
            hoverBackgroundColor: "rgb(54, 192, 235)",
          },
        ],
      },
      options: {
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      },
    });
    /*-- Chart of Deaths Cases --*/
    var myChartDeaths = new Chart(ctxDesths, {
      type: "bar",
      data: {
        labels: ["Total Confirmed", "Total Deaths"],
        datasets: [
          {
            label: "Total",
            data: [this.stats.TotalConfirmed, this.stats.TotalDeaths],
            fill: true,
            backgroundColor: "rgba(255, 99, 132, 0.2)",
            borderColor: "rgb(255, 99, 132)",
            tension: 0.1,
            borderWidth: 1,
            hoverBackgroundColor: "rgb(230, 56, 56)",
          },
        ],
      },
      options: {
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      },
    });
    console.log(myChart);
    console.log(myChartDeaths);
  },
};
</script>
