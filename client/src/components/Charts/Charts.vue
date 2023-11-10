
<template>
    <div class="container">
      <canvas id="mychart" width="100%" height="50px"></canvas>
    </div>
  </template>
 
  <script>
  import Chart from 'chart.js/auto';
  import ChartData from '../../charts/chartOptions.js'
 
  export default {
    name: 'MyChart',
    props: ['chartInput', 'chartType'],
    data() {
      return {
        ChartData: ChartData,
        graphData: {
          labels: this.chartInput['chartLabels'],
          datasets: [
            {
              label: this.chartInput['chartTitle'],
              data: this.chartInput['chartValues'],
              backgroundColor: [
              'rgba(54, 162, 235, 0.5)', // Example color 1
              'rgba(255, 99, 132, 0.5)', // Example color 2
              'rgba(75, 192, 192, 0.5)', // Example color 3
              // Add more colors as needed
            ],
            borderColor: [
              'rgba(54, 162, 235, 1)',
              'rgba(255, 99, 132, 1)',
              'rgba(75, 192, 192, 1)',
            ],
              borderWidth: 3
            }
          ]
        },
        options: {
          responsive: true,
          tooltips: {
            intersect: false,
            node: "index",
          },
        },
      }
    },
    mounted() {
    this.createChart();
  },
  watch: {
    chartType: 'createChart', // Watch for changes in chartType
  },
  methods: {
    createChart() {
      const ctx = document.getElementById('mychart');
      new Chart(ctx, {
        type: this.chartType, // Use the selected chart type
        data: this.graphData,
        options: this.ChartData.options,
      });
    },
  },
  }
  </script>