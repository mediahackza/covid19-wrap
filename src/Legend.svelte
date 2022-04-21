<script>
  import { fills } from './fills.js'
  import * as d3 from 'd3'
  $: scaleX = d3.scaleLinear().domain([0, 5]).range([0, 55])
</script>

<div class="intro">
  <p>
    <span class="firstcharacter">O</span>n 5 March 2020, South Africa recorded
    the first positive Covid-19 case. A few days later the first Covid-related
    death was confirmed in KwaZulu-Natal. Over the next two years the world was
    ravaged by SARS-CoV-2, or "coronavirus". In South Africa, more than 100,000
    deaths were attributed to coronavirus. But the real death toll is likely to
    be three times higher. Estimates of "excess deaths” show that deaths from
    natural causes over this two-year period were far higher than expected (see
    below).
  </p>
  <p>
    Over two years Media Hack collected <a
      href="https://mediahack.co.za/datastories/coronavirus/dashboard/"
      target="_blank">detailed data on coronavirus</a
    > in South Africa.
  </p>
  <div class="credits">
    <span class="bold">Design & Development</span>:
    <a href="https://twitter.com/alastairotter" target="_blank"
      >Alastair Otter</a
    >
    &nbsp;
    <span class="bold">Data</span>:
    <a href="https://mediahack.co.za" target="_blank">Media Hack Collective</a>
  </div>
</div>

<div class="four-waves">
  <div class="section-title">The Changing Face of a Pandemic</div>
  <div class="section-sub-title">March 2020 &mdash; March 2022</div>
</div>
<div class="legend">
  <div class="legend-block legend-left">
    <div class="legend-text-title">Four Waves</div>

    The first confirmed cases of coronavirus were reported in March 2020 and, as
    the virus spread, the daily cases increased so that by June the country was
    experiencing its first major wave.
    <p>
      In the chart below the triangles represent a day's worth of data, the
      larger the triangle, the more confirmed cases were reported on that day.
      The colour of the triangle represents the number of reported deaths on a
      day. The <span class="highlight-pink">darker the pink</span>, the higher
      the number of deaths.
    </p>
    <p>
      Daily Covid-related deaths in the first wave started to peak in late July
      2020 and continued to be high until September. The second wave, which was
      dominated by the Beta variant of the virus, peaked in late January 2021.
      The largest number of daily deaths of the whole two-year period occurred
      in January 2021.
    </p>
    <p>
      Deaths were more evenly distributed throughout the third wave than in the
      second wave. This is very different to the fourth wave which saw
      significant testing and an increase in daily cases but relatively low
      numbers of daily deaths.
    </p>
  </div>
  <div class="legend-block legend-center legend-no-border">
    <!-- <div class="legend-title">Reading this chart</div> -->
    <div class="legend-row">
      <div class="svg">
        <svg>
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            transform="
            translate({scaleX(1)} 24)
            scale(0.10)"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            transform="
            translate({scaleX(2)} 16)
            scale(0.15)"
          />

          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            transform="
            translate({scaleX(3)} 8)
            scale(0.2)"
          />

          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            transform="
            translate({scaleX(4)} 0)
            scale(0.25)"
          />
          <text class="legend-label" x="0" y="52">0</text>
          <text class="legend-label" x="85" y="52">200</text>
        </svg>
      </div>
      <div class="legend-text">
        <div class="legend-text-title">Confirmed Cases</div>
        The size of each triangle represents the number of confirmed cases on a single
        day.
      </div>
    </div>

    <!-- Legend Row Two -->
    <div class="legend-row">
      <div class="svg">
        <svg
          ><path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
            translate({scaleX(5)} 0)
            scale(0.25)"
            style="fill: {fills[5]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
            translate({scaleX(4)} 0)
            scale(0.25)"
            style="fill: {fills[4]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
            translate({scaleX(3)} 0)
            scale(0.25)"
            style="fill: {fills[3]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
          translate({scaleX(2)} 0)
          scale(0.25)"
            style="fill: {fills[2]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
        translate({scaleX(1)} 0)
        scale(0.25)"
            style="fill: {fills[1]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
        translate({scaleX(0)} 0)
        scale(0.25)"
            style="fill: {fills[0]};"
          />

          <text class="legend-label" x="0" y="52">0</text>
          <text class="legend-label" x="85" y="52">800</text>
        </svg>
      </div>
      <div class="legend-text">
        <div class="legend-text-title">Reported Deaths</div>
        The colour of each triangle represents the number of Covid-related deaths
        reported for a day.
      </div>
    </div>

    <!-- LEGEND ROW 3 -->
    <div class="legend-row">
      <div class="svg">
        <svg
          ><path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-height"
            transform="
            translate(30 0)
            scale(0.15)"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-height"
            transform="
            translate(30 15)
            scale(0.15)"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-height"
            transform="
            translate(30 30)
            scale(0.15)"
          />
          <text class="legend-label legend-label-center" x="90" y="10"
            >100,000</text
          >
          <!-- <text class="legend-label legend-label-center" x="70" y="60">200</text> -->
        </svg>
      </div>
      <div class="legend-text">
        <div class="legend-text-title">Daily Tests</div>
        The height of each triangle represents the number of Covid-related tests
        done in a day.
      </div>
    </div>
    <p class="footnote">
      Note: The dates for cases and deaths are the dates on which they were
      reported by the department of health and not necessarily the actual date
      of test or death.
    </p>
  </div>
  <div class="legend-block legend-right  legend-no-border">
    <!-- <div class="legend-title">&nbsp;</div> -->

    <!-- LEGEND RIGHT -- ---------------------------------------------------->
  </div>
</div>

<style>
  .bold {
    font-weight: 700;
    color: #fff;
  }
  .credits {
    margin-top: 30px;
    width: 100%;
    text-align: center;
    text-transform: uppercase;
    /* color: #fff; */
    font-weight: 300;
    font-size: 0.8rem;
    font-family: 'Inter', Arial, Helvetica, sans-serif;
  }
  .four-waves {
    border-top: solid 1px gray;
  }
  .highlight-pink {
    color: hotpink;
    font-weight: 700;
    padding: 2px 3px;
    /* color: #000; */
  }
  .intro {
    width: 90%;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
    font-size: 1rem;
    line-height: 1.4rem;
    padding-bottom: 50px;
    /* border-bottom: solid 1px gray; */
    /* margin-bottom: 25px; */
    font-family: 'Inter', Arial, Helvetica, sans-serif;
  }
  .legend {
    width: 100%;
    margin-left: auto;
    margin-right: auto;

    font-size: 0.95rem;
    line-height: 1.3rem;
    font-family: 'Roboto Condensed', Arial, Helvetica, sans-serif;
    font-weight: 300;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    border-bottom: solid 1px rgb(156, 156, 156);
    padding-bottom: 10px;
    padding-top: 50px;
    border-bottom: dashed 1px rgb(78, 78, 78);
    /* border-top: solid 5px indianred; */
    margin-top: 0px;
    margin-bottom: 20px;
    padding-bottom: 30px;
  }

  .legend-right {
    /* border: none; */
    padding-left: 0px;
  }

  .legend-label {
    fill: gray;
    font-size: 0.7rem;
    font-family: 'Roboto Condensed', Arial, Helvetica, sans-serif;
  }
  .legend-label-center {
    text-anchor: middle;
  }

  .firstcharacter {
    float: left;
    font-family: Georgia;
    font-size: 75px;
    line-height: 60px;
    padding-top: 4px;
    padding-right: 8px;
    padding-left: 3px;
    color: #fff;
    color: inherit;
    /* font-weight: 700; */
  }
  .triangle {
    fill: #3f5efba8;
    /* opacity: 0.4; */
    stroke: #000;
    stroke-width: 3px;
  }

  svg {
    overflow: visible;
    height: 70px;
    width: 110px;
    /* border: solid 1px lightgray; */
  }

  .legend-row {
    /* border: solid 10px lightgray; */
    position: relative;
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
  .legend-text {
    padding-top: 0px;
    margin-bottom: 10px;
  }

  .triangle-color {
    opacity: 0.4;
  }

  .triangle-height {
    fill: #3f5efb;
    opacity: 0.6;
    stroke: #000;
    stroke-width: 3px;
  }
  .footnote {
    font-size: 0.8rem;
    font-weight: 300;
    color: gray;
  }

  @media only screen and (max-width: 600px) {
    .legend {
      grid-template-columns: 1fr;
    }
    .legend-block {
      border-right: none;
      padding-right: 0px;
    }
  }
</style>
