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



	console.log(top60)


	let cities = top60.top60

	export let chartwidth;
	if (window.innerWidth > 601) {
		chartwidth = Math.min(320, ((window.innerWidth-20)/3))
	} else {
		chartwidth = window.innerWidth
	}

	console.log(chartwidth)


</script>

<style>
	div.grid {
		width:100%;
		display: grid;
		grid-template-columns: auto;
		grid-column-gap: 0;
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
<p>People are walking and driving more now than they were in January, but transit usage is nearly half of what it was.</p>
<p>The below data was released by Apple, using requests for Apple Maps directions. Each line measures the percentage change of requests for the three modes, measured from a mid-January baseline. Across the entire United States, requests for driving directions are up 34% from mid-January, and walking directions are up 18%. But transit routings tell a different story, down 47% in that same time period.</p>
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
