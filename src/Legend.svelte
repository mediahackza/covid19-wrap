<script>
  import { fills } from './fills.js'
  import * as d3 from 'd3'
  $: scaleX = d3.scaleLinear().domain([0, 5]).range([0, 40])
</script>

<div class="legend">
  <div class="legend-block legend-left">
    <span class="firstcharacter">O</span>n 5 March 2020 South Africa recorded
    the first positive Covid-19 cases was recorded in South Africa. The first
    recorded deaths was XXXX days later on XX March 2020 in KwaZulu-Natal. The
    chart below visualises two years of the pandemic in South African from 7
    March 2020 through to 7 March 2022.
  </div>
  <div class="legend-block legend-center">
    <div class="legend-title">Reading this chart</div>
    <div class="legend-row">
      <div class="svg">
        <svg
          ><path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            transform="
            translate(30 0)
            scale(0.2 0.2)"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            transform="
            translate(15 9)
           
            scale(0.15 0.145)"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle"
            transform="
            translate(0 16)
            scale(0.1 0.1)"
          />
          <text class="legend-label" x="0" y="48">0</text>
          <text class="legend-label" x="55" y="48">200</text>
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
            scale(0.15)"
            style="fill: {fills[5]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
            translate({scaleX(4)} 0)
            scale(0.15)"
            style="fill: {fills[4]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
            translate({scaleX(3)} 0)
            scale(0.15)"
            style="fill: {fills[3]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
          translate({scaleX(2)} 0)
          scale(0.15)"
            style="fill: {fills[2]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
        translate({scaleX(1)} 0)
        scale(0.15)"
            style="fill: {fills[1]};"
          />
          <path
            d="M92.3315 0.918335L184.194 160.03H0.468575L92.3315 0.918335Z"
            class="triangle triangle-color"
            transform="
        translate({scaleX(0)} 0)
        scale(0.15)"
            style="fill: {fills[0]};"
          />

          <text class="legend-label" x="0" y="40">0</text>
          <text class="legend-label" x="55" y="40">200</text>
        </svg>
      </div>
      <div class="legend-text">
        <div class="legend-text-title">Reported Deaths</div>
        The colour of each triangle represents the number of Covid-related deaths
        reported for a day.
      </div>
    </div>
  </div>
  <div class="legend-block legend-right">
    <div class="legend-title">&nbsp;</div>

    <!-- LEGEND RIGHT -- ---------------------------------------------------->
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
          <text class="legend-label legend-label-center" x="43" y="-5">0</text>
          <text class="legend-label legend-label-center" x="43" y="70">200</text
          >
        </svg>
      </div>
      <div class="legend-text">
        <div class="legend-text-title">Daily Tests</div>
        The height of each triangle represents the number of Covid-related tests
        done in a day.
      </div>
    </div>
  </div>
</div>

<style>
  .legend {
    width: 94%;
    margin-left: auto;
    margin-right: auto;
    color: gray;
    font-size: 0.8rem;
    line-height: 1.1rem;
    font-family: 'Roboto', Arial, Helvetica, sans-serif;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 0px;
    border-bottom: solid 1px rgb(156, 156, 156);
    padding-bottom: 10px;
    padding-top: 10px;
    border-top: solid 5px rgb(219, 219, 219);
    margin-top: 20px;
  }
  .legend-block {
    border-right: solid 1px rgb(53, 53, 53);
    padding: 5px 20px 20px;
  }
  .legend-right {
    border: none;
  }
  .legend-center {
    border: none;
  }
  .legend-title {
    text-transform: uppercase;
    color: #fff;
    font-size: 0.7rem;
    font-weight: 700;

    margin-bottom: 10px;
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
    color: indianred;
    float: left;
    font-family: Georgia;
    font-size: 75px;
    line-height: 60px;
    padding-top: 4px;
    padding-right: 8px;
    padding-left: 3px;
  }
  .triangle {
    fill: #3f5efba8;
    /* opacity: 0.4; */
    stroke: #000;
    stroke-width: 3px;
  }

  svg {
    overflow: visible;
    height: 55px;
    width: 90px;
    /* border: solid 1px lightgray; */
  }
  .legend-row * {
    display: inline;
  }
  .legend-row {
    /* border: solid 10px lightgray; */
    position: relative;
  }
  .legend-text {
    /* border: solid 1px lightgray; */
    position: absolute;
    top: 0%;
  }
  .triangle-color {
    opacity: 0.4;
  }
  .legend-text-title {
    display: block;
    color: indianred;
    font-weight: 700;
    font-size: 0.7rem;
    text-transform: uppercase;
  }
  .triangle-height {
    fill: #3f5efb;
    opacity: 0.6;
    stroke: #000;
    stroke-width: 3px;
  }
</style>
