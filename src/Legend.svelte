<script>
  import { fills } from './fills.js'
  import * as d3 from 'd3'
  $: scaleX = d3.scaleLinear().domain([0, 5]).range([0, 55])
</script>

<div class="intro">
  <p>
    <span class="firstcharacter">O</span>n 5 March 2020 South Africa recorded
    the first postive Covid-19 case in the country. A few days later the first
    Covid-related death was confirmed in KwaZulu-Natal. Over the next two years
    South Africa and the world was ravaged by "coronavirus" and more than
    100,000 deaths were directly attributed to coronavirus. But many more deaths
    [NUMBER] are likely to be closer to the truth if we look at estimates of
    "excess deaths" which show death numbers far in excess of predicted numbers
    over this two year period (see below).
  </p>
  <p>
    Over two years Media Hack collected <a
      href="https://mediahack.co.za/datastories/coronavirus/dashboard/"
      target="_blank">detailed data on coronavirus</a
    > in South Africa.
  </p>
  <div class="credits">
    <span class="bold">Design & Development</span>: Alastair Otter &nbsp;
    <span class="bold">Data</span>: Media Hack Collective
  </div>
</div>

<div class="four-waves">
  <div class="section-title">The changing face of a pandemic</div>
  <div class="section-sub-title">March 2020 &mdash; March 2022</div>
</div>
<div class="legend">
  <div class="legend-block legend-left">
    <div class="legend-text-title">Four Waves</div>

    The first confirmed cases of coronavirus were reported in March and April
    2020 and the first major wave started in June. In the chart below the
    triangles represent a day's worth of data. The first large number of deaths
    occured in late July through to September. The second wave peaked in late
    January 2021 with the largest number of daily deaths in mid-January (the<span
      class="highlight-pink">darker the pink color</span
    >
    the more deaths recorded on a day).

    <p>
      Daily deaths were more evenly distributed throughout the third wave than
      in the second wave. This is very different to the fourth wave which saw
      signficant testing and an increase in daily cases but relatively low
      numbers of daily deaths.
    </p>
    <p class="footnote">
      Note: The dates for cases and deaths are the dates on which they were
      reported by the dpartment of health and not cessarily the exact date of
      test or death.
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
    font-size: 0.9rem;
    line-height: 1.3rem;
    padding-bottom: 25px;
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
