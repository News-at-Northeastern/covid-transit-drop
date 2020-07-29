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
	// import * as jsondata from '../public/datasets/parkland.json'
	// import * as linetestdata from '../public/datasets/linetestdata.json'
	import * as mobility from '../public/datasets/applemobility.json'
	import * as tests from '../public/datasets/linetestdata.json'

	console.log(mobility.default)


	let cities = ["New York City", "Washington DC", "Boston", "San Francisco - Bay Area", "Chicago", "Philadelphia", "Seattle", "Baltimore", "Pittsburgh", "Hartford", "New Haven", "Minneapolis", "Portland", "Buffalo", "Miami"]


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
{#if mobility}
	{#each cities as city}
		<LineChart
			width={width * 0.33}
			height={width * 0.33 * 0.66}
			data={mobility.default}
			title={city}
			xVar={"date"}
			lineA={city + "-driving"}
			lineB={city + "-walking"}
			lineC={city + "-transit"}
		/>
	{/each}
{/if}
<GraphicFooter
	source={"Apple Maps"}
	note={"Data for May 11-12 is not available."}
/>
