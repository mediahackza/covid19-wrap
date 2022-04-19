<script>
  let width = 900
  let height = 300
  import * as d3 from 'd3'
  import { vaccinations } from './data/vaccinations.js'
  let dateParse = d3.timeParse('%d-%m-%Y')
  let dateParseTwo = d3.timeParse('%Y-%m-%d')
  let dateFormat = d3.timeFormat('%Y-%m-%d')

  vaccinations.forEach((d) => {
    d.date = dateParse(d.date)
  })

  $: scaleX = d3
    .scaleTime()
    .domain(d3.extent(vaccinations, (d) => d.date))
    .range([50, width])

  $: scaleY = d3
    .scaleLinear()
    .domain([0, 300000])
    .range([height - 30, 30])

  $: line = d3
    .line()
    .x((d) => scaleX(d.date))
    .y((d) => scaleY(d.average))

  console.log(vaccinations)
</script>

<div class="vaccinations-wrap">
  <div class="section-title">Vaccinations</div>
  <div class="section-sub-title">February 2021 - April 2022</div>

  <div class="legend legend-vaccinations">
    <div class="legend-block">
      On 5 March 2020 South Africa recorded the first positive Covid-19 cases
      was recorded in South Africa. The first recorded deaths was XXXX days
      later on XX March 2020 in KwaZulu-Natal. The chart below visualises two
      years of the pandemic in South African from 7 March 2020 through to 7
      March 2022.
    </div>
    <div class="legend-block legend-no-border">
      <div class="vaccinations-legend">
        <div>
          <div class="daily-line" />
        </div>
        <div>Daily vaccinations</div>

        <div>
          <div class="average-line" />
        </div>
        <div>7-day Average vaccinations</div>
      </div>
    </div>
  </div>

  <div class="vaccinations-chart" bind:clientWidth={width}>
    <svg {width} {height}>
      <defs>
        <linearGradient id="grad2" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop
            offset="0%"
            style="stop-color:rgb(255, 105, 180, 0.3);stop-opacity:1"
          />
          <stop offset="100%" style="stop-color:#3c5bf100;stop-opacity:1" />
        </linearGradient>

        <linearGradient id="grad3" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop
            offset="0%"
            style="stop-color:rgb(255, 105, 180, 0.9);stop-opacity:1"
          />
          <stop offset="100%" style="stop-color:#00000050;stop-opacity:1" />
        </linearGradient>
      </defs>
      <line
        x1="40"
        y1={scaleY(50000)}
        x2={width}
        y2={scaleY(50000)}
        class="grid-line grid-line-bold"
      />

      <line
        x1="40"
        y1={scaleY(100000)}
        x2={width}
        y2={scaleY(100000)}
        class="grid-line grid-line-bold"
      />
      <line
        x1="40"
        y1={scaleY(150000)}
        x2={width}
        y2={scaleY(150000)}
        class="grid-line"
      />
      <line
        x1="40"
        y1={scaleY(200000)}
        x2={width}
        y2={scaleY(200000)}
        class="grid-line"
      />
      <line
        x1="40"
        y1={scaleY(250000)}
        x2={width}
        y2={scaleY(250000)}
        class="grid-line"
      />
      <line
        x1="40"
        y1={scaleY(300000)}
        x2={width}
        y2={scaleY(300000)}
        class="grid-line"
      />
      {#each vaccinations as v}
        <rect
          width="1"
          height={height - 30}
          class="bar-invert"
          x={scaleX(v.date)}
          y={0}
        />

        <rect
          width="1"
          height={height - scaleY(v.daily) - 30}
          class="bar"
          x={scaleX(v.date)}
          y={scaleY(v.daily)}
        />

        <path d={line(vaccinations)} class="average-line" />
      {/each}
      <text x="40" y={scaleY(50000) + 4} class="y-axis">50k</text>
      <text x="40" y={scaleY(100000) + 4} class="y-axis">100k</text>
      <text x="40" y={scaleY(150000) + 4} class="y-axis">150k</text>
      <text x="40" y={scaleY(200000) + 4} class="y-axis">200k</text>
      <text x="40" y={scaleY(250000) + 4} class="y-axis">250k</text>
      <text x="40" y={scaleY(300000) + 4} class="y-axis">300k</text>

      <text
        x={scaleX(dateParseTwo('2021-12-05')) + 5}
        y={height - 245}
        class="date-labels"
      >
        5 Dec 2021
      </text>
      <line
        x1={scaleX(dateParseTwo('2021-12-05'))}
        y1={height - 150}
        x2={scaleX(dateParseTwo('2021-12-05'))}
        y2={height - 250}
        class="marker-line"
      />
      <!--    -->
      <line
        x1={scaleX(dateParseTwo('2021-08-27'))}
        y1={height - 200}
        x2={scaleX(dateParseTwo('2021-08-27'))}
        y2={height - 270}
        class="marker-line"
      />
      <text
        x={scaleX(dateParseTwo('2021-08-27')) + 5}
        y={height - 265}
        class="date-labels"
      >
        27 Aug 2021
      </text>
      <line
        x1={scaleX(dateParseTwo('2022-01-01'))}
        y1={height - 50}
        x2={scaleX(dateParseTwo('2022-01-01'))}
        y2={height - 150}
        class="marker-line"
      />

      <text
        x={scaleX(dateParseTwo('2022-01-01')) + 5}
        y={height - 145}
        class="date-labels"
      >
        1 Jan 2022
      </text>

      <line
        x1={scaleX(dateParseTwo('2021-05-01'))}
        y1={height - 35}
        x2={scaleX(dateParseTwo('2021-05-01'))}
        y2={height - 125}
        class="marker-line"
      />

      <text
        x={scaleX(dateParseTwo('2021-05-01')) + 5}
        y={height - 120}
        class="date-labels"
      >
        1 Jan 2021
      </text>
    </svg>
  </div>
</div>

<style>
  .daily-line {
    width: 50px;
    height: 3px;
    background: hotpink;
    transform: translate(0, 10px);
    margin-right: 10px;
  }
  .average-line {
    width: 50px;
    height: 3px;
    background: #fff;
    transform: translate(0, 10px);
    margin-right: 10px;
  }
  .vaccinations-legend {
    display: grid;
    grid-template-columns: auto 2fr;
  }
  .marker-line {
    stroke: #fff;
    stroke-width: 2px;
    stroke-dasharray: 3, 3;
  }
  .legend-vaccinations {
    margin-top: 30px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    padding: 0px;
    border: none;
    margin-bottom: 30px;
  }
  .legend-block {
    /* border: none; */
    /* padding: 0px; */
  }
  .dummy {
    fill: rgb(255, 105, 180);
    fill: #3c5bf1;
  }
  /* .y-axis {
    fill: gray;
    text-anchor: end;
    font-size: 0.8rem;

    font-family: 'Roboto', Arial, Helvetica, sans-serif;
  } */
  .average-line {
    fill: none;
    stroke: #fff;
    stroke-width: 2px;
  }
  .bar {
    /* fill: #3c5bf1; */
    /* fill: none; */
    /* fill: hotpink; */
    /* fill: #000; */
    /* fill: #ffff; */
    /* fill: #000; */
    fill: hotpink;
  }
  .bar-invert {
    /* fill: rgba(255, 105, 180, 0.406); */
    /* fill: hotpink; */
    /* fill: rgba(30, 143, 255, 0.47); */
    fill: none;
  }
  .vaccinations-wrap {
    width: 100%;
    padding-bottom: 50px;
    border-top: solid 3px rgb(62, 62, 62);
  }
  svg {
    /* border: solid 1px gray; */
    overflow: visible;
  }
  .date-labels {
    fill: #fff;
    font-size: 0.7rem;
  }
</style>
