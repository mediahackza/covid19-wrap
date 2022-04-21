<script>
  import { excess } from './data/excess-deaths.js'
  console.log(excess)
  let width = 900
  let height = 300
  import * as d3 from 'd3'
  let dateParse = d3.timeParse('%Y-%m-%d')
  let dateFormat = d3.timeFormat('%Y-%m-%d')

  excess.forEach((d) => {
    d.date = dateParse(d.date)
  })

  $: scaleX = d3
    .scaleTime()
    .domain(d3.extent(excess, (d) => d.date))
    .range([50, width])

  $: scaleY = d3.scaleLinear().domain([0, 30000]).range([height, 0])

  $: line = d3
    .area()
    .x((d) => scaleX(d.date))
    .y1((d) => scaleY(d.excess_deaths))
    .y0((d) => scaleY(0))

  $: lineFill = d3
    .area()
    .x((d) => scaleX(d.date))
    .y1((d) => scaleY(d.excess_deaths))
    .y0((d) => scaleY(d.prediction))

  $: lineFillBottom = d3
    .area()
    .x((d) => scaleX(d.date))
    .y0((d) => scaleY(d.prediction))
    .y1((d) => scaleY(0))

  $: linePrediction = d3
    .area()
    .x((d) => scaleX(d.date))
    .y1((d) => scaleY(d.prediction))
    .y0((d) => scaleY(0))

  $: linePredictionLine = d3
    .line()
    .x((d) => scaleX(d.date))
    .y((d) => scaleY(d.prediction))

  $: lineHigher = d3
    .line()
    .x((d) => scaleX(d.date))
    .y((d) => scaleY(d.higher))

  $: lineLower = d3
    .line()
    .x((d) => scaleX(d.date))
    .y((d) => scaleY(d.lower))

  $: lineRange = d3
    .area()
    .x((d) => scaleX(d.date))
    .y0((d) => scaleY(d.lower))
    .y1((d) => scaleY(d.higher))

  // .curve(curveStep)
</script>

<div class="excess">
  <div class="section-title">Calculating the Real Cost</div>
  <div class="section-sub-title">March 2020 &mdash; February 2022</div>

  <div class="legend legend-excess">
    <div />
    <div class="legend-block legend-no-border">
      <p>
        Officially, 100,000 people died of Covid-related causes over the past
        two years. But in reality many more are likely to have died as a result
        of the pandemic. The SA Medical Research Council estimates that there
        were <a
          href="https://www.samrc.ac.za/reports/report-weekly-deaths-south-africa"
          target="_blank">just over 300,000 "excess deaths"</a
        >, which is the number of deaths by natural causes above the number that
        would be expected if there wasn’t a pandemic. Most of the excess deaths
        are likely to have been Covid-related.
      </p>

      <p>
        In the chart below the dotted white line shows the predicted number of
        deaths from natural causes based on historical data, the dark pink area
        shows deaths below the predicted number and the bright pink area
        represents excess deaths.
      </p>
    </div>
  </div>

  <div class="excess-chart" bind:clientWidth={width}>
    <svg {width} {height}>
      <line
        x1="50"
        y1={scaleY(5000)}
        x2={width}
        y2={scaleY(5000)}
        class="grid-line"
      />
      <line
        x1="50"
        y1={scaleY(10000)}
        x2={width}
        y2={scaleY(10000)}
        class="grid-line"
      />
      <line
        x1="50"
        y1={scaleY(15000)}
        x2={width}
        y2={scaleY(15000)}
        class="grid-line"
      />
      <line
        x1="50"
        y1={scaleY(20000)}
        x2={width}
        y2={scaleY(20000)}
        class="grid-line"
      />
      <line
        x1="50"
        y1={scaleY(25000)}
        x2={width}
        y2={scaleY(25000)}
        class="grid-line"
      />
      <!-- <path
        d={lineHigher(excess)}
        fill="none"
        stroke="hotpink"
        stroke-width="3"
        class="excess-lines excess-higher" -->
      />
      <!-- <path
        d={lineLower(excess)}
        fill="none"
        stroke="limegreen"
        stroke-width="3"
        class="excess-lines excess-lower"
      /> -->
      <path d={lineFillBottom(excess)} class="excess-area excess-area-bottom" />
      <path d={lineFill(excess)} class="excess-area" />

      <path d={line(excess)} class="excess-area-line" style="fill: hotpink;" />

      <path d stroke-width="13" class="excess-lines excess-range" />

      <path
        d={linePredictionLine(excess)}
        stroke-width="3"
        class="excess-lines excess-prediction-line"
      />

      <path
        d={linePrediction(excess)}
        stroke-width="3"
        class="excess-lines excess-prediction"
      />

      <text x="40" y={scaleY(0) + 4} class="y-axis">0</text>
      <text x="40" y={scaleY(5000) + 4} class="y-axis">5,000</text>
      <text x="40" y={scaleY(10000) + 4} class="y-axis">10,000</text>
      <text x="40" y={scaleY(15000) + 4} class="y-axis">15,000</text>
      <text x="40" y={scaleY(20000) + 4} class="y-axis">20,000</text>
      <text x="40" y={scaleY(25000) + 4} class="y-axis">25,000</text>

      <!-- DATES -->
      <line
        class="x-grid"
        x1={scaleX(dateParse('2020-07-15'))}
        y1={height}
        x2={scaleX(dateParse('2020-07-15'))}
        y2={30}
      />
      <text class="x-axis" x={scaleX(dateParse('2020-07-15'))} y={height + 20}>
        15 Jul 2020</text
      >

      <line
        class="x-grid"
        x1={scaleX(dateParse('2021-01-10'))}
        y1={height}
        x2={scaleX(dateParse('2021-01-10'))}
        y2={30}
      />
      <text class="x-axis" x={scaleX(dateParse('2021-01-10'))} y={height + 20}>
        10 Jan 2021</text
      >

      <line
        class="x-grid"
        x1={scaleX(dateParse('2021-07-12'))}
        y1={height}
        x2={scaleX(dateParse('2021-07-12'))}
        y2={30}
      />
      <text class="x-axis" x={scaleX(dateParse('2021-07-12'))} y={height + 20}>
        12 Jul 2021</text
      >

      <line
        class="x-grid"
        x1={scaleX(dateParse('2021-12-25'))}
        y1={height}
        x2={scaleX(dateParse('2021-12-25'))}
        y2={30}
      />
      <text class="x-axis" x={scaleX(dateParse('2021-12-25'))} y={height + 20}>
        25 Dec 2021</text
      >

      <!-- Labels -->
      <line
        x1="90"
        x2="140"
        y1={height - 50}
        y2={height - 50}
        class="predicted-legend">Predicted Deaths</line
      >
      <text x="150" y={height - 45} class="on-chart-label"
        >Predicted Deaths</text
      >

      <text
        x={scaleX(dateParse('2020-12-15'))}
        y={100}
        class="on-chart-label weekly-deaths">Weekly Deaths</text
      >
    </svg>
  </div>
</div>

<style>
  .predicted-legend {
    stroke-width: 2px;
    stroke: #fff;
    stroke-dasharray: 6, 3;
  }
  .on-chart-label {
    fill: #fff;
    font-weight: 700;
    font-size: 0.8rem;
    paint-order: stroke;
    stroke-width: 5px;
    stroke: #000;
  }
  .weekly-deaths {
    fill: hotpink !important;
    paint-order: stroke;
    stroke-width: 5px;
    stroke: #000;
    text-anchor: end;
  }
  .x-grid {
    stroke: rgba(182, 182, 182, 0.749);
    stroke: #181818;
    stroke-width: 0.1rem;
    /* stroke-dasharray: 5, 5; */
    shape-rendering: crispEdges;
  }
  .x-axis {
    fill: gray;
    font-size: 0.8rem;
    text-anchor: middle;
  }
  /* .y-axis {
    fill: gray;
    text-anchor: end;
  } */

  .excess-chart {
    /* width: 94%; */
    margin-left: auto;
    margin-right: auto;
    padding-bottom: 100px;
  }
  .excess {
    border-top: solid 4px rgb(41, 41, 41);
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    /* border: solid 1px red; */
  }
  svg {
    margin: 0px;
  }
  .excess-lines {
    /* opacity: 0.5; */
    /* stroke-width: 1px; */
  }
  .excess-area {
    fill: rgba(255, 105, 180);
    fill: none;
    /* stroke: rgb(253, 0, 127); */
    stroke-width: none;
  }
  .excess-area-bottom {
    fill: rgba(255, 80, 165, 0.48);
  }
  .excess-area-line {
    /* fill: rgba(32, 32, 32, 0.37); */
    fill: none;
    /* stroke: hotpink; */
    /* stroke-width: 4px; */
  }
  .excess-higher,
  .excess-lower {
    /* stroke-dasharray: 3, 3;
    stroke: #fff; */
    /* stroke: none; */
  }
  .excess-range {
    fill: none;
    stroke: gray;
    /* opacity: 0.5; */
    stroke-width: 1px;
    shape-rendering: crispEdges;
    stroke-dasharray: 3, 3;
    stroke-width: 1px;
  }
  .excess-prediction {
    /* stroke-dasharray: 6, 3; */

    stroke-width: 0px;
    stroke: #fff;
    fill: rgba(0, 0, 0, 0.692);
    stroke: none;
    /* stroke: none; */
  }
  .excess-prediction-line {
    stroke-dasharray: 6, 3;
    stroke-width: 5px;
    stroke: #fff;
    fill: none;
  }
  .legend-excess {
    margin-top: 30px;
    display: grid;
    grid-template-columns: 1fr 3fr 1fr;
  }

  svg {
    overflow: visible;
  }
</style>
