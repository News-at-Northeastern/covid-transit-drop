<script>
	import { onMount, afterUpdate } from 'svelte';
	import BarChart from './charts/BarChart.svelte'
	import GraphicTitle from './components/GraphicTitle.svelte'
	import GraphicFooter from './components/GraphicFooter.svelte'
	import * as jsondata from '../public/datasets/data.json'
	// import * as jsondata from '//news.northeastern.edu/interactive/2020/11/covid-states-issues/datasets/data.json'

	let dataset;

	let groups_age = ["18-29", "30-44", "45-64", "65+"];
	let groups_party = ["Democrats", "Republicans", "Independents"];
	let groups_race = ["White", "Hispanic", "African American", "Asian American"]
	let selectoptions = [
		{id: 0, text: "Age Cohort", array: groups_age},
		{id: 1, text: "Political Party", array: groups_party},
		{id: 2, text: "Race", array: groups_race},
	]
	$: active = 1;



	onMount(function() {
		dataset = jsondata.default
	})

	afterUpdate(function() {
		console.log(selectoptions[active].array)
	})

	let width = Math.min(
		document.getElementById('interactive').getBoundingClientRect().width,
		1000
	);

	function chartwidth(x) {
		if (window.innerWidth >= 600) {
			return (width / x)
		} else {
			return width
		}
	}


</script>

<style>
	:global(div.chart) {
		display:inline;
	}

	:global(form) {
		display:inline;

	}

	:global(form select) {
		font-size:1.25rem;
		font-family: "Akkurat", sans-serif;
		padding:0.5rem 0.2rem;
	}

	:global(#interactive-filter) {
		display:block;
		width: 100%;
		text-align:center;
		margin:0 0 2rem;
		font-size:1.1rem;
	}

</style>

<GraphicTitle
	title={"Most important problem facing the nation"}
/>
{#if dataset && dataset.length > 0}
	<div id="interactive-filter">
		<span>View most common responses based on: </span>
		<form>
			<select bind:value={active}>
				{#each selectoptions as opt}
					<option value={opt.id}>
						{opt.text}
					</option>
				{/each}
			</select>
		</form>
	</div>
	{#if active > -1}
	{#each selectoptions[active].array as item (item)}
		<BarChart
			width={chartwidth((selectoptions[active].array).length)}
			height={220}
			data={dataset.filter(d => {
				return d.demographic === item
			})}
			grouping={item}
			xVar={"ranking"}
			yVar={"percentage"}
		/>
	{/each}
	{/if}
{/if}
<GraphicFooter
	source={"The COVID-19 Consortium for Understanding the Public's Policy Preferences Across States. covidstates.org."}
	note={active}
/>
