<script>
  let width = 900
  let height = 300
  import * as d3 from 'd3'
  import { vaccinations } from './data/vaccinations.js'
  import { vaxxed } from './data/vaxpercent.js'
  let dateParse = d3.timeParse('%d-%m-%Y')
  let dateParseTwo = d3.timeParse('%Y-%m-%d')
  let dateFormat = d3.timeFormat('%Y-%m-%d')

  vaccinations.forEach((d) => {
    d.date = dateParse(d.date)
  })
  vaxxed.forEach((d) => {
    d.Date = dateParseTwo(d.Date)
    d.date = d.Date
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

  $: scaleYVax = d3
    .scaleLinear()
    .domain([0, 50])
    .range([height - 30, 30])

  $: lineVaxxed = d3
    .line()
    .x((d) => scaleX(d.date))
    .y((d) => scaleYVax(d['percent_total_population_fully_vaxxed']))
</script>

<div class="vaccinations-wrap">
  <div class="section-title">Vaccinations</div>
  <div class="section-sub-title">February 2021 - April 2022</div>

  <div class="legend legend-vaccinations">
    <div class="legend-block">
      South Africa started vaccinating healthcare workers on 18 February 2021
      with the one-dose Johnson & Johnson (J&J) vaccine. The official
      vaccination rollout to the public started on 17 May 2021 with people over
      60 years old getting the two-dose Pfizer vaccine. By 19 April 2022, more
      than 34-million doses of vaccine had been administered, both J&J and
      Pfizer, and close to a third of the population was fully vaccinated.
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
        <div>7-day average vaccinations</div>
      </div>
    </div>
  </div>

  <div class="vaccinations-chart" bind:clientWidth={width}>
    <svg {width} {height}>
      <line
        x1="40"
        y1={scaleY(50000)}
        x2={width}
        y2={scaleY(50000)}
        class="grid-line"
      />

      <line
        x1="40"
        y1={scaleY(100000)}
        x2={width}
        y2={scaleY(100000)}
        class="grid-line"
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

        <path
          d={line(vaccinations)}
          class="average-line"
          style="transform: translate(0, -2px);"
        />
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
        x1={scaleX(dateParseTwo('2021-05-17'))}
        y1={height - 45}
        x2={scaleX(dateParseTwo('2021-05-17'))}
        y2={height - 150}
        class="marker-line"
      />
      <text
        x={scaleX(dateParseTwo('2021-05-17')) + 5}
        y={height - 145}
        class="date-labels"
      >
        17 May 2021
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
        x1={scaleX(dateParseTwo('2021-02-24'))}
        y1={height - 35}
        x2={scaleX(dateParseTwo('2021-02-24'))}
        y2={height - 125}
        class="marker-line"
      />

      <text
        x={scaleX(dateParseTwo('2021-02-24')) + 5}
        y={height - 120}
        class="date-labels"
      >
        24 Feb 2021
      </text>

      <!-- <path d={lineVaxxed(vaxxed)} class="vax-line" /> -->
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
  .vax-line {
    fill: none;
    stroke: #fff;
  }
  @media only screen and (max-width: 600px) {
    .legend-vaccinations {
      grid-template-columns: 1fr;
    }
  }
</style>
