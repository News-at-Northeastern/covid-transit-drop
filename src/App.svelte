<script>
	import { onMount } from 'svelte';
	import HoverCArd from './components/HoverCard.svelte'
	import BarChart from './charts/BarChart.svelte'
	import LineChart from './charts/MultiLineChart.svelte'
	import Map from './charts/Map.svelte'
	import GraphicTitle from './components/GraphicTitle.svelte'
	import GraphicFooter from './components/GraphicFooter.svelte'
	import { group, groups } from 'd3-array'

	import * as top60 from './helpers/top60.js'
	import * as mobility from '../public/datasets/applemobility.json'

	let cities = top60.top60

	export let chartwidth;
	export let chartheight;
	if (window.innerWidth > 601) {
		chartwidth = Math.min(320, ((document.getElementById("interactive").offsetWidth-20)/3));
		chartheight = chartwidth * 0.75;
	} else {
		chartwidth = ((document.getElementById("interactive").offsetWidth-3)/2);
		chartheight = chartwidth;
	}


</script>

<style>
	div.grid {
		width:100%;
		display: grid;
		grid-template-columns: auto auto;
		grid-column-gap: 0px;
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
	width={chartwidth}
/>
<div class="grid" id="grid-container">
{#if mobility}
	{#each cities as city}
		<div class="grid-item">
			<LineChart
				width={chartwidth}
				height={chartheight}
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
	source={'DATA: Apple Maps. ICONS: <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik, Flaticon</a>.'}
	note={"The data was assembled by Apple, using requests for directions made by Apple Maps users. Each line measures the percentage change of requests for the three modes of transportation, measured from a mid-January baseline."}
/>
