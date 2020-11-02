<script>
	import { onMount, afterUpdate } from 'svelte';
	import { scaleLinear, scaleBand } from 'd3-scale';
	import { axisLeft, axisRight, axisTop, axisBottom } from 'd3-axis';
	import { select } from 'd3-selection';
	import { colors } from '../helpers/colors.js'

	let d3 = {
		scaleLinear: scaleLinear,
		scaleBand: scaleBand,
		select: select,
		axisLeft: axisLeft,
		axisRight: axisRight,
		axisBottom: axisBottom,
		axisTop: axisTop
	}

	let el;

	const padding = { top: 10, right: 25, bottom: 35, left: 10 };


		export let data = {data};
		export let width = {width};
		export let height = {height};
		export let xVar = {xVar};
		export let yVar = {yVar};
		export let grouping = {grouping};

	$: xScale = d3.scaleLinear()
		.domain([0, 40])
		.range([0, width - padding.left - padding.right]);

	$: yScale = d3.scaleBand()
		.domain(data.map(function(o) { return o[xVar]; }))
		.rangeRound([padding.top, height - padding.bottom])
		.padding(0.2);





	// onMount(generateBarChart);
	afterUpdate(generateBarChart);

	function generateBarChart() {
		// console.log(data)

		var svg = d3.select(el)
			.append("svg")
			.attr("width", width)
			.attr("height", height)
			.append("g")
			.attr("transform",
				  "translate(" + padding.left + "," + padding.top + ")");

		svg.append('g')
			.append('text')
			.text(grouping)
			.attr('x', width/2)
			.attr('y', 3)
			.attr('text-anchor', 'middle')
			.attr('class', 'charttitle')

		let datagroups = svg.append('g')
	    .selectAll("rect")
	    .data(data)
	    .enter();

	    datagroups.append("rect")
			 .attr("y", function (d) { return yScale(d[xVar]); })
		    .attr("x", function (d) { return 0; })
			 .attr("height", yScale.bandwidth())
			 .attr("width", function (d) { return xScale(d[yVar]); })
			 .attr("fill", colors[grouping]);

		datagroups.append("text")
			.attr("class", "barlabel")
			.attr("y", function (d) { return yScale(d[xVar]) + (yScale.bandwidth()/1.5); })
			.attr("x", function (d) { return xScale(d[yVar]); })
			.text(function(d) { return " " + d.issue + ": " + d.percentage + "% " })
			.attr("text-anchor", function(d) {
				if (d.percentage > 28) {
					return "end"
				} else {
					return "start"
				}
			})
			.attr("fill", function(d) {
				if (d.percentage > 28) {
					return "white"
				} else {
					return "#888"
				}
			})

		 // axes
		 svg.append("g")
			 .attr("transform", "translate(0," + (height-padding.bottom) + ")")
			 .call(d3.axisBottom(xScale).ticks(3));

		 svg.append("g")
				 .call(d3.axisLeft(yScale).tickSize(0));
	}
</script>

<style>
	.chart :global(rect) {

	}

	:global(text.charttitle) {
		text-transform: uppercase;
		font-size:0.9rem;
	}

	:global(text.barlabel) {
		font-size:0.7rem;
	}
</style>

<div bind:this={el} class="chart"></div>
