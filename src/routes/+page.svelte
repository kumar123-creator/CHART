<script>
	import { onMount } from 'svelte';
	import { Chart, ColumnSeries, Category } from '@syncfusion/ej2-charts';
	import { Browser } from '@syncfusion/ej2-base';
	Chart.Inject(ColumnSeries, Category);
  
	onMount(async () => {
	  // Make an HTTP request to fetch data from the API
	  const apiUrl = 'https://api.recruitly.io/api/dashboard/sales/data/opportunitymonthlyusermetrics?start=01%2F10%2F2022&end=01%2F10%2F2023&apiKey=TEST45684CB2A93F41FC40869DC739BD4D126D77';
	  const response = await fetch(apiUrl);
	  const data = await response.json();
  
	  // Process the API response data to format it for the chart
	  const chartData = data.map(item => ({
		x: item.monthLabel,  // Assuming "monthLabel" is the X-axis value
		y: item['Andy Barnes']  // Use the name of the series as the Y-axis value
	  }));
      console.log(chartData);
	  const chart = new Chart({
		primaryXAxis: {
		  valueType: 'Category',
		  majorGridLines: { width: 0 }
		},
		primaryYAxis: {
		  labelFormat: '{value}',
		  title: 'Oppurtunity Value ',
		  edgeLabelPlacement: 'Shift',
		  majorTickLines: { width: 0 },
		  lineStyle: { width: 0 },
		},
		series: [
		  {
			type: 'Column',
			dataSource: chartData,
			xName: 'x',
			width: 2,
			yName: 'y',
			name: 'Andy Barnes',
			columnSpacing: 0.1,
		  },
		],
	  });
  
	  chart.appendTo('#container');
	});
  </script>
  
  <body>
	<h2>Oppurtunity Value by User</h2>
	<div id='container'></div>
  </body>
  
  <style>
	h2 {
    text-align: center;
    margin: 20px 0;
  }
  </style>
  