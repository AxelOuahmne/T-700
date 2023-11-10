
<template>
    <div class="container">
      <canvas id="mychart"></canvas>
    </div>
  </template>
 
  <script>
  import Chart from 'chart.js/auto';
  import ChartData from '../../charts/chartOptions.js'
 
  export default {
    name: 'MyChart',
    props:['chartInput'],
    data() {
      return {
        ChartData: ChartData,
        graphData: {
          labels: this.chartInput['chartLabels'],
          datasets: [
            {
              label: this.chartInput['chartTitle'],
              data: this.chartInput['chartValues'],
              backgroundColor: "rgba(221,255,221)",
              borderColor: "#36495d",
              borderWidth: 3
            }
          ]
        },
      }
    },
    mounted() {
      const ctx = document.getElementById('mychart');
      new Chart(ctx, {
      type: this.ChartData.type,
      data: this.graphData,
      options: this.ChartData.options
    }
      );
    }
  }
  </script>