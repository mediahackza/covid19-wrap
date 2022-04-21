<script>
  let showNotes = true
  import Legend from './Legend.svelte'
  import Title from './Title.svelte'
  import Maps from './Maps.svelte'
  import Excess from './Excess.svelte'
  import Vaccinations from './Vaccinations.svelte'
  import { fills } from './fills.js'
  let dates = [
    { date: '01-03-2020', month: 'Mar 2020' },
    { date: '01-06-2020', month: 'Jun 2020' },
    { date: '01-09-2020', month: 'Sep 2020' },
    { date: '01-12-2020', month: 'Dec 2020' },
    { date: '01-03-2021', month: 'Mar 2021' },
    { date: '01-06-2021', month: 'Jun 2021' },
    { date: '01-09-2021', month: 'Sep 2021' },
    { date: '01-12-2021', month: 'Dec 2021' },
    { date: '01-03-2022', month: 'Mar 2022' },
  ]

  // let notes = [
  //   {
  //     date: '10-07-2020',
  //     note: '10 July 2020',
  //     line: true,
  //     tests: 45000,
  //   },
  //   {
  //     date: '14-01-2021',
  //     note: '14 January 2021',
  //     line: true,
  //     tests: 60000,
  //   },

  //   {
  //     date: '03-07-2021',
  //     note: '3 July 2021',
  //     line: true,
  //     tests: 75729,
  //   },

  //   {
  //     date: '11-12-2021',
  //     note: '11 December 2021',
  //     line: true,
  //     tests: 90000,
  //   },
  // ]

  import { fly, fade, scale, slide, blur } from 'svelte/transition'
  let height = 400
  let width = 600

  import { onMount } from 'svelte'
  import * as d3 from 'd3'

  let dateParse = d3.timeParse('%d-%m-%Y')
  let dateFormat = d3.timeFormat('%Y-%m-%d')

  let cumulative = []

  dates.forEach((d) => {
    d.date = dateParse(d.date)
  })

  $: scaleX = d3
    .scaleTime()
    .domain(d3.extent(cumulative, (d) => d.date))
    .range([10, width - 10])

  $: scaleY = d3
    .scaleLinear()
    .domain(d3.extent(cumulative, (d) => d.tests_daily * 1.3))
    .range([height, 0])

  $: scaleR = d3
    .scaleLinear()
    .domain(d3.extent(cumulative, (d) => d.cases_daily))
    .range([10, 30])

  $: scaleT = d3
    .scaleLinear()
    .domain(d3.extent(cumulative, (d) => d.cases_daily))
    .range([0.1, 0.5])

  $: scaleF = d3
    .scaleLinear()
    .domain(d3.extent(cumulative, (d) => d.deaths_daily))
    .range([0, 5])

  async function getCumulative() {
    await fetch(
      'https://mediahack.co.za/datastories/coronavirus/api/cumulative.php'
    )
      .then((response) => response.json())
      .then((response) => {
        response.forEach((d) => {
          d.date = dateParse(d.date)
          d.cumulative_cases = +d.cumulative_cases
          d.cases_daily = +d.cases_daily
          d.tests_daily = +d.tests_daily
          d.deaths_daily = +d.deaths_daily
        })
        cumulative = response.filter((d) => d.tests_daily > 0)
      })
  }

  onMount(() => {
    getCumulative()
  })
</script>

<main>
  <Title />
  <Legend />
  <!-- <div class="tooltip">Tooltip</div> -->
  <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
    <!-- <div
      class="controls {showNotes ? 'controls-on' : ''}"
      on:click={() => (showNotes = !showNotes)}
    >
      Show Notes
    </div> -->
    <svg {width} {height}>
      {#each dates as date}
        <text x={scaleX(date.date) - 10} y="30" class="dates">{date.month}</text
        >
        <line
          x1={scaleX(date.date)}
          y1="40"
          x2={scaleX(date.date)}
          y2={height - 50}
          class="axis-line"
        />
      {/each}
      {#each cumulative as data, i}
        <!-- <circle
          transition:slide={{ x: -200, delay: i * 3, duration: 2000 }}
          cx={scaleX(data.date)}
          cy={scaleY(data.tests_daily)}
          r={scaleR(data.cases_daily)}
          class="circle"
        /> -->
        <!-- <circle
          transition:slide={{ x: -200, delay: i * 3, duration: 2000 }}
          cx={scaleX(data.date)}
          cy={scaleY(data.tests_daily)}
          r={scaleR(data.deaths_daily)}
          class="circle-blue"
        /> -->
        <g
          transform="
                translate({scaleX(data.date)}, {scaleY(data.tests_daily)})
                scale({scaleT(data.cases_daily)})"
          transform-origin="-13 -100"
        >
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            style=" fill: {fills[scaleF(data.deaths_daily).toFixed(0)]}"
            on:mouseover={() => console.log(data)}
            on:focus={() => console.log(data)}
          />
        </g>
        <!-- <line
          x1={scaleX(data.date)}
          y1={scaleY(0)}
          x2={scaleX(data.date)}
          y2={scaleY(data.tests_daily)}
          class="line"
          style="stroke: lightgray; stroke-width: 1px; opacity: 0.5;"
        /> -->
      {/each}

      <!-- Ntable events -->
      <!-- <g id="events">
        {#each notes as note}
          {#if note.line && showNotes}
            <path
              d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
              transform="
              translate({scaleX(dateParse(note.date)) + 8} {scaleY(note.tests) -
                140})
              rotate(90)
              scale(0.05)"
              style="fill: #fff;"
            />
            <line
              x1={scaleX(dateParse(note.date))}
              y1={scaleY(note.tests) - 90}
              y2={scaleY(note.tests) - 140}
              x2={scaleX(dateParse(note.date))}
              class="note-line"
            />
            <text
              x={scaleX(dateParse(note.date)) + 12}
              y={scaleY(note.tests) - 133}
              class="notes">{note.note}</text
            >
          {/if}
          {#if !note.line && showNotes}
            <text
              x={scaleX(dateParse(note.date)) - 2}
              y={scaleY(note.tests) - 50}
              class="notes">{note.note}</text
            >
          {/if}
        {/each}
      </g> -->
    </svg>
  </div>

  <!-- MAPS -->

  <Maps />

  <!-- Excess Deaths -->
  <Excess />

  <!-- Vaccinations -->
  <Vaccinations />

  <div class="social">
    If you enjoyed this please share: <br />
    <a
      href="https://twitter.com/intent/tweet?text=A%20visualisation%20of%20two%20years%20of%20Covid%20in%20South%20Africa%20by%20@alastairotter%20.%20https://covid.theoutlier.co.za%20#ddj"
      target="_blank"><img src="/twitter.svg" alt="Share to Twitter" /></a
    >&nbsp;<a
      href="https://www.facebook.com/sharer/sharer.php?u=https://covid.theoutlier.co.za"
      target="_blank"><img src="/facebook.svg" alt="Share to Facebook" /></a
    >
  </div>

  <div class="cta">
    <div class="cta-inner">
      <div class="cta-text">
        Subscribe to our newsletter for more data stories. The newsletter is
        sent out every two weeks.
      </div>
      <form
        class="js-cm-form"
        id="subForm"
        action="https://www.createsend.com/t/subscribeerror?description="
        method="post"
        data-id="92D4C54F0FEC16E5ADC2B1904DE9ED1AAA5D68D26FD222ECE64C6A563A9BF339160E857807618A1E6614A43A746C409629B4C258EC846CC82657DA43FB662EAD"
        _lpchecked="1"
      >
        <input
          autocomplete="Email"
          aria-label="Email"
          class="js-cm-email-input qa-input-email top-newsletter"
          id="fieldEmail"
          maxlength="200"
          name="cm-jtdujtk-jtdujtk"
          required=""
          type="email"
          placeholder="Your Email Address"
        /><input
          aria-label="Signup source"
          id="fieldjthyqu"
          maxlength="200"
          name="cm-f-jthyqu"
          type="hidden"
          value="covid-wrap"
        />
        <button class="top-submit-button">Subscribe</button>
      </form>
      <script
        type="text/javascript"
        src="https://js.createsend1.com/javascript/copypastesubscribeformlogic.js"></script>
      <div class="cta-text">
        Send comments, questions to <a href="mailto:info@mediahack.co.za"
          >info@mediahack.co.za</a
        >.<br />Follow us:
        <a href="https://twitter.com/outlierafrica"
          ><img src="/twitter.svg" alt="twitter-link" /> @outlierafrica</a
        >
      </div>
      <div class="cta-text cta-small">
        Every effort has been made to ensure that the data and information in
        this story is accurate. Please let me know if you find anything I've
        missed. Or just tell me what you thought of this piece. You can find me
        on <a href="https://twitter.com/alastairotter" target="_blank"
          >Twitter</a
        >
        or email me:
        <a href="mailto:alastair@mediahack.co.za">alastair@mediahack.co.za</a>.
        I'd love to hear from you.
      </div>
    </div>
  </div>
</main>

<style>
  svg {
    overflow: visible;
  }
  main {
    width: 100%;
    /* max-width: 1200px; */
    margin: auto;
    max-width: 1100px;
  }
  .chart {
    width: 100%;
    height: 90vh;
    max-height: 550px;
    min-height: 500px;
    margin-left: auto;
    margin-right: auto;
    position: relative;
    /* border: solid 1px #eee; */
  }
  .controls {
    position: absolute;
    top: 50px;
    left: 10px;
    color: gray;
    background: #131313;
    padding: 5px 10px;
    border: solid 1px gray;
    font-size: 0.7rem;
    text-transform: uppercase;
    font-family: 'Roboto', Arial, Helvetica, sans-serif;
    cursor: pointer;
  }
  .controls:hover {
    background: #3f3f3f;
    color: #fff;
  }
  .controls-on {
    background: #3f3f3f;
    color: #fff;
  }
  .controls-on:hover {
    background: #131313;
    color: gray;
  }
  .circle,
  .circle-blue {
    fill: rgba(255, 105, 180, 0.222);
    stroke: rgba(255, 255, 255, 0.384);
    stroke-width: 1;
  }
  .circle-blue {
    fill: rgba(0, 0, 250, 0.222);
    stroke: rgba(255, 255, 255, 0.384);
    stroke-width: 1;
  }
  .circle:hover {
    fill: rgb(250, 97, 174);
  }
  .triangle {
    /* stroke: hotpink; */
    stroke: none;
    stroke-width: 6px;
    width: 30px;
    height: 30px;
    /* fill: rgba(148, 40, 94, 0.479); */
    opacity: 0.4;
  }
  .triangle:hover {
    /* opacity: 1; */
  }
  .dates {
    fill: gray;
    font-size: 0.7rem;
    text-transform: uppercase;
  }
  .axis-line {
    stroke: gray;
    stroke-width: 1px;
    opacity: 0.5;
    stroke-dasharray: 2, 2;
  }
  .notes {
    fill: lightgray;
    font-family: 'Roboto Condensed', Arial, Helvetica, sans-serif;
    text-transform: uppercase;
    font-size: 0.8rem;
    paint-order: stroke;
    stroke-width: 5px;
    stroke: #131313;
    /* font-weight: 700; */
    /* display: none; */
  }
  .note-line {
    stroke: lightgray;

    stroke-width: 0.5px;
    shape-rendering: crispEdges;
  }
  .cta {
    width: 100%;
    text-align: center;
    font-size: 0.8rem;
    padding-bottom: 50px;
    border-top: solid 1px gray;
    padding-top: 0px;
    font-weight: 400;
    font-family: 'Inter', Arial, Helvetica, sans-serif;
    text-transform: uppercase;
    color: gray;
  }
  .cta-inner {
    max-width: 500px;
    margin-left: auto;
    margin-right: auto;
  }
  .cta-text {
    margin-bottom: 20px;
    line-height: 1.3rem;
    margin-top: 20px;
    line-height: 2rem;
  }
  .cta input {
    background: rgb(54, 54, 54);
    border: solid 1px gray;
    color: #fff;
    font-size: 0.9rem;
  }
  .cta button {
    background: #c4c4a3;
    border: none;
    color: #000;
    text-transform: uppercase;
    margin-left: 10px;
    padding: 5px 20px;
    border-radius: 10px;
    font-size: 0.8rem;
    cursor: pointer;
    font-weight: 700;
  }
  .cta button:hover {
    background: #dcdcb4;
  }
  .cta img {
    width: 15px;
  }
  .cta a {
    /* color: #1d9bf0; */
  }
  .social {
    /* margin-top: 20px; */
    font-size: 0.8rem;
    width: 100%;
    text-align: center;
    text-transform: uppercase;
    margin-bottom: 50px;
    font-family: 'Inter', Arial, Helvetica, sans-serif;
    color: #c4c4a3;
  }
  .social img {
    transform: translate(0px, 3px);
    width: 30px;
  }
  .cta-small {
    font-size: 0.8rem;
    line-height: 1.1rem;
    text-transform: initial;
  }
  @media only screen and (max-width: 600px) {
    main {
      width: 90%;
    }
  }
</style>
