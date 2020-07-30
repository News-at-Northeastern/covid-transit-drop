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

	export let width = 300;


</script>

<style>
	div.grid {
		width:100%;
		display: grid;
		grid-template-columns: auto;
		grid-column-gap: 0;
	}

	@media only screen and (min-width:600px) {
		div.grid {
			grid-template-columns: auto auto;
			grid-column-gap: 20px;
		}
	}

	@media only screen and (min-width:900px) {
		div.grid {
			grid-template-columns: auto auto auto;
			grid-column-gap: 20px;
		}
	}

</style>

<GraphicTitle
	title={"How travel patterns have changed in 2020, in 60 U.S. cities"}
	subhed={"A look at something etc"}
/>
<div class="grid" id="grid-container">
{#if mobility}
	{#each cities as city}
		<div class="grid-item"  bind:clientWidth={width}>
			<LineChart
				width={width}
				height={width * 0.75}
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
