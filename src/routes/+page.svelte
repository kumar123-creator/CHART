<script>
	import { onMount } from "svelte";
	import * as Chart from "@syncfusion/ej2-charts";
	import {DataLabel} from "@syncfusion/ej2-charts";

	let chartData = [];

	const fetchChartData = async () => {
		try {
			const response = await fetch(
				"https://api.recruitly.io/api/dashboard/sales/data/opportunitymonthlyusermetrics?start=01%2F10%2F2022&end=01%2F10%2F2023&apiKey=TEST45684CB2A93F41FC40869DC739BD4D126D77"
			);
			const data = await response.json();
			 chartData = data; // Make chartData reactive
			 console.log(chartData);
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
						yName: "0", // Adjust for the actual field name in your data
						name: "Bob Shaw",
						type: "Line",
					},
					{
						dataSource: chartData,
						xName: "monthLabel",
						yName: "10", // Adjust for the actual field name in your data
						name: "Andy Barnes",
						type: "Line",
					},
					{
						dataSource: chartData,
						xName: "monthLabel",
						yName: "0", // Adjust for the actual field name in your data
						name: "Gary Williams",
						type: "Line",
					},
				],
				primaryXAxis: {
					title: "Month",
				},
				primaryYAxis: {
					title: "Opportunity Value",
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
  