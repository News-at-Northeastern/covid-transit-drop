<script>
	import { onMount } from 'svelte';
	import HoverCArd from './components/HoverCard.svelte'
	import BarChart from './charts/BarChart.svelte'
	import LineChart from './charts/MultiLineChart.svelte'
	import Map from './charts/Map.svelte'
	import GraphicTitle from './components/GraphicTitle.svelte'
	import GraphicFooter from './components/GraphicFooter.svelte'
	import { group, groups } from 'd3-array'

	// gather data set. the Rollup JSON plugin loads everything with key "default", hence the second line below. (also filtering to California only)
	import * as jsondata from '../public/datasets/parkland.json'
	import * as linetestdata from '../public/datasets/linetestdata.json'
	import * as mobility from '../public/datasets/applemobility.json'
	let dataset = jsondata.default.filter(d => {
		return d.city.indexOf(", CA") > -1
	})

	let cities = ["Boston", "Houston", "Austin"]


	export let width = Math.min(
		document.getElementById('interactive').getBoundingClientRect().width,
		1000
	);
</script>

<style>
	div.chart {
		display: inline;
	}
</style>

<GraphicTitle
	title={"Today's chart"}
	subhed={"A look at something etc"}
/>
{#each cities as city}
<h3>{city + "-driving"}</h3>
	<LineChart
		width={width * 0.33}
		height={width * 0.33 * 0.66}
		data={mobility}
		xVar={"date"}
		lineA={city + "-driving"}
		lineB={city + "-walking"}
		lineC={city + "-transit"}
	/>
{/each}
<!-- <BarChart
	width={width}
	height={width * 0.66}
	data={dataset}
	xVar={"city"}
	yVar={"population"}
/> -->
<!-- <HoverCard
	data={dataset}
	xVar={"city"}
	yVar={"population"}
/> -->
<GraphicFooter
	source={"The Trust for Public Land"}
	note={"Data includes the top 100 cities by population in the US"}
/>
