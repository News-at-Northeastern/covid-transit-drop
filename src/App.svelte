<script>
	import { onMount } from 'svelte';
	import HoverCArd from './components/HoverCard.svelte'
	import BarChart from './charts/BarChart.svelte'
	import LineChart from './charts/MultiLineChart.svelte'
	import Map from './charts/Map.svelte'
	import GraphicTitle from './components/GraphicTitle.svelte'
	import GraphicFooter from './components/GraphicFooter.svelte'
	import * as top60 from './helpers/top60.js'
	import { group, groups } from 'd3-array'

	// gather data set. the Rollup JSON plugin loads everything with key "default", hence the second line below. (also filtering to California only)
	// import * as jsondata from '../public/datasets/parkland.json'
	// import * as linetestdata from '../public/datasets/linetestdata.json'
	import * as mobility from '../public/datasets/applemobility.json'
	import * as tests from '../public/datasets/linetestdata.json'




	let cities = top60.top60

	export let chartwidth;
	if (window.innerWidth > 601) {
		chartwidth = Math.min(320, ((document.getElementById("interactive").offsetWidth-20)/3))
	} else {
		chartwidth = ((document.getElementById("interactive").offsetWidth-20)/2)
	}


</script>

<style>
	div.grid {
		width:100%;
		display: grid;
		grid-template-columns: auto auto;
		grid-column-gap: 20px;
	}

	.grid-item {
		margin-top: .8em !important;
	}

	@media only screen and (min-width:601px) {
		div.grid {
			grid-template-columns: auto auto auto;
			grid-column-gap: 20px;
		}
	}

</style>

<GraphicTitle
	title={"How travel patterns have changed in 2020, in 60 U.S. cities"}
	subhed={""}
/>
<div class="grid" id="grid-container">
{#if mobility}
	{#each cities as city}
		<div class="grid-item">
			<LineChart
				width={chartwidth}
				height={chartwidth * 0.75}
				data={mobility.default}
				title={city}
				xVar={"date"}
				lineA={city + "-driving"}
				lineB={city + "-walking"}
				lineC={city + "-transit"}
			/>
		</div>
	{/each}
{/if}
</div>
<GraphicFooter
	source={"Apple Maps"}
	note={"Data runs from January 13 to July 28. Data for May 11-12 is not available."}
/>
