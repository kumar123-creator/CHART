<script>
	import { onMount } from "svelte";
	import * as Chart from "@syncfusion/ej2-charts";
  
	let chartData = [];
  
	const fetchChartData = async () => {
	  try {
		const response = await fetch(
		  "https://api.recruitly.io/api/dashboard/sales/data/opportunitymonthlyusermetrics?start=01%2F10%2F2022&end=01%2F10%2F2023&apiKey=TEST45684CB2A93F41FC40869DC739BD4D126D77"
		);
		const data = await response.json();
		chartData = data;
		createChart();
	  } catch (error) {
		console.error("Error fetching chart data", error);
	  }
	};
  
	const createChart = () => {
	  const chartElement = document.getElementById("chart");
	  if (chartElement) {
		new Chart.Chart({
		  // Chart configuration
		  series: [
			{
			  dataSource: chartData,
			  xName: "monthLabel",
			  yName: "Andy Barnes", // Adjust for other series
			  name: "Andy Barnes",
			  type: "Line",
			},
			// Add more series for other users if needed
		  ],
		  primaryXAxis: {
			title: "Month",
		  },
		  primaryYAxis: {
			title: "Oppurtunity Value",
		  },
		}).appendTo(chartElement);
	  }
	};
  
	onMount(() => {
	  fetchChartData();
	});
  </script>
  
  <style>
	  #chart {
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
  }

  /* Add styles for the chart title */
  h2 {
    text-align: center;
    margin: 20px 0;
  }
  </style>
  <h2>Sales Chart</h2>
  <div id="chart" style="height: 300px;"></div>
  