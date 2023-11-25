<template>
    <LineChart
      :chart-data="data"
      :options="options"
      css-classes="chart-container"
    />
  </template>
  
  <script setup>
  import { ref, computed } from "vue"
  import { LineChart } from "vue-chart-3"
  import {
    Chart,
    LineController,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement
  } from "chart.js"
  
  Chart.register(
    LineController,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement
  )
  
  const salesData = [
  { month: "January", sales: 150 },
  { month: "February", sales: 120 },
  { month: "March", sales: 210 },
  { month: "April", sales: 150 },
  { month: "May", sales: 190 },
  { month: "June", sales: 260 },
  { month: "July", sales: 150 },
  { month: "August", sales: 120 },
  { month: "September", sales: 210 },
  { month: "October", sales: 160 },
  { month: "November", sales: 200 },
  { month: "December", sales: 280 },
];
  
  const data = computed(() => ({
    labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sept", "Oct", "Nov","Dec"],
  
    datasets: [
    {
        label: "Revenue",
        data: salesData.map((data) => data.sales),
        borderColor: "#32de84",
        borderWidth: 3,
        pointBorderColor: "#006400",
        pointBorderWidth: 3,
        tension: 0.5,
        fill: true,
        backgroundColor: (context) => {
          const ctx = context.chart.ctx;
          const gradient = ctx.createLinearGradient(0, 0, 0, 300);
          gradient.addColorStop(0, "#66FF00");
          gradient.addColorStop(1, "white");
          return gradient;
        },
      },
    ]
  }))
  
  const options = {
    plugins: {
      legend: true,
    },
    responsive: true,
    scales: {
      y: {
        ticks: {
          font: {
            size: 17,
            weight: "bold",
          },
        },
        title: {
          display: true,
          text: "Sales",
          padding: {
            bottom: 10,
          },
          font: {
            size: 30,
            style: "italic",
            family: "Arial",
          },
        },
        min: 50,
      },
      x: {
        ticks: {
          font: {
            size: 17,
            weight: "bold",
          },
        },
        title: {
          display: true,
          text: "Month",
          padding: {
            top: 10,
          },
          font: {
            size: 30,
            style: "italic",
            family: "Arial",
          },
        },
      },
    },
  };
  </script>