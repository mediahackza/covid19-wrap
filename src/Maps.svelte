<script>
  import { provDeaths } from './data/provinces-deaths.js'
  import { fills2 } from './fills.js'
  import * as d3 from 'd3'

  let deathsMax = d3.max(provDeaths, (d) => d.monthly_deaths)

  $: scale = d3.scaleLinear().domain([0, deathsMax]).range([0, 5])

  let mar2020 = provDeaths.filter((d) => d.year === 2020 && d.month === 'March')
  let apr2020 = provDeaths.filter((d) => d.year === 2020 && d.month === 'April')

  let may2020 = provDeaths.filter((d) => d.year === 2020 && d.month === 'May')
  let jun2020 = provDeaths.filter((d) => d.year === 2020 && d.month === 'June')
  let jul2020 = provDeaths.filter((d) => d.year === 2020 && d.month === 'July')
  let aug2020 = provDeaths.filter(
    (d) => d.year === 2020 && d.month === 'August'
  )
  let sept2020 = provDeaths.filter(
    (d) => d.year === 2020 && d.month === 'September'
  )
  let oct2020 = provDeaths.filter(
    (d) => d.year === 2020 && d.month === 'October'
  )
  let nov2020 = provDeaths.filter(
    (d) => d.year === 2020 && d.month === 'November'
  )
  let dec2020 = provDeaths.filter(
    (d) => d.year === 2020 && d.month === 'December'
  )

  let jan2021 = provDeaths.filter(
    (d) => d.year === 2021 && d.month === 'January'
  )
  let feb2021 = provDeaths.filter(
    (d) => d.year === 2021 && d.month === 'February'
  )

  let mar2021 = provDeaths.filter((d) => d.year === 2021 && d.month === 'March')
  let apr2021 = provDeaths.filter((d) => d.year === 2021 && d.month === 'April')
  let may2021 = provDeaths.filter((d) => d.year === 2021 && d.month === 'May')
  let jun2021 = provDeaths.filter((d) => d.year === 2021 && d.month === 'June')
  let jul2021 = provDeaths.filter((d) => d.year === 2021 && d.month === 'July')
  let aug2021 = provDeaths.filter(
    (d) => d.year === 2021 && d.month === 'August'
  )
  let sept2021 = provDeaths.filter(
    (d) => d.year === 2021 && d.month === 'September'
  )
  let oct2021 = provDeaths.filter(
    (d) => d.year === 2021 && d.month === 'October'
  )
  let nov2021 = provDeaths.filter(
    (d) => d.year === 2021 && d.month === 'November'
  )
  let dec2021 = provDeaths.filter(
    (d) => d.year === 2021 && d.month === 'December'
  )

  // let mapData = [
  //   {
  //     ec: fills2[0],
  //     fs: fills2[1],
  //     gp: fills2[2],
  //     wc: fills2[3],
  //     kzn: fills2[4],
  //     lp: fills2[5],
  //     //   mp: fills2[5],
  //     //   nc: fills2[5],
  //     //   nw: fills2[5],
  //     mp: '#000',
  //     nc: '#000',
  //     nw: '#000',
  //   },
  // ]

  import Map from './Map.svelte'
</script>

<div class="maps-outer-wrap">
  <div class="section-title">Countrywide Deaths</div>
  <div class="section-sub-title">March 2020 &mdash; February 2022</div>
  <div class="map-legend">
    <div class="legend-block map-legend-left">
      The first confirmed Covid case was recorded in KwaZulu-Natal in April 2020
      but it wasn't until June and July that the number of daily deaths started
      to rise, peaking in August 2020.The second and third waves had a major
      impact on the Eastern and Western Cape as well as Gauteng.
    </div>
    <div class="legend-block map-legend-right  legend-no-border">
      Provinces with more than 100 confirmed coronavirus-related deaths per
      month
      <div class="map-legend-bar">
        <div class="bar" style="background: #2B2B2B;" />
        <div class="bar" style="background: {fills2[0]};" />
        <div class="bar" style="background: {fills2[1]};" />
        <div class="bar" style="background: {fills2[2]};" />
        <div class="bar" style="background: {fills2[3]};" />
        <div class="bar" style="background: {fills2[4]};" />
        <div class="bar" style="background: {fills2[5]};" />
        <div class="bar" style="background: {fills2[6]};" />
        <div class="bar" style="background: {fills2[7]};" />

        <div class="bar bar-text">&lang;100</div>
        <div class="bar bar-text">100+</div>
        <div class="bar bar-text" />
        <div class="bar bar-text" />
        <div class="bar bar-text" />
        <div class="bar bar-text" />
        <div class="bar bar-text" />
        <div class="bar bar-text" />
        <div class="bar bar-text">4,000+</div>
      </div>
    </div>
  </div>
  <div class="map-wrap">
    <Map mapData={mar2020} mapMonth="March 2020" />

    <Map mapData={apr2020} mapMonth="April 2020" />
    <Map mapData={may2020} mapMonth="May 2020" />
    <Map mapData={jun2020} mapMonth="June 2020" />
    <Map mapData={jul2020} mapMonth="July 2020" />
    <Map mapData={aug2020} mapMonth="August 2020" />
    <Map mapData={sept2020} mapMonth="September 2020" />
    <Map mapData={oct2020} mapMonth="October 2020" />
    <Map mapData={nov2020} mapMonth="November 2020" />
    <Map mapData={dec2020} mapMonth="December 2020" />
    <Map mapData={jan2021} mapMonth="January 2021" />
    <Map mapData={feb2021} mapMonth="February 2021" />
    <Map mapData={mar2021} mapMonth="March 2021" />
    <Map mapData={apr2021} mapMonth="April 2021" />
    <Map mapData={may2021} mapMonth="May 2021" />
    <Map mapData={jun2021} mapMonth="June 2021" />
    <Map mapData={jul2021} mapMonth="July 2021" />
    <Map mapData={aug2021} mapMonth="August 2021" />
    <Map mapData={sept2021} mapMonth="September 2021" />
    <Map mapData={oct2021} mapMonth="October 2021" />
    <Map mapData={nov2021} mapMonth="November 2021" />
    <Map mapData={dec2021} mapMonth="December 2021" />
    <Map mapData={dec2020} mapMonth="January 2022" />
    <Map mapData={dec2020} mapMonth="February 2022" />
  </div>
</div>

<style>
  .map-wrap {
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
    /* border: solid 1px #fff; */
    padding-bottom: 100px;

    padding-top: 20px;
  }
  .maps-outer-wrap {
    padding-top: 20px;
    border-top: solid 4px rgb(41, 41, 41);
  }
  .maps-title {
    border-top: solid 5px rgb(156, 156, 156);
    font-family: Georgia, 'Times New Roman', Times, serif;
    font-size: 1.4rem;
    color: #fff;
    width: 100%;
    text-align: center;
    width: 94%;
    margin-left: auto;
    margin-right: auto;
    padding-top: 30px;
  }
  .maps-sub-title {
    font-family: Georgia, 'Times New Roman', Times, serif;
    font-size: 1.4rem;
    color: #fff;
    width: 100%;
    text-align: center;
  }
  .map-legend {
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    display: grid;
    grid-template-columns: 2fr 2fr;
    grid-gap: 30px;
    border-bottom: dashed 1px rgb(78, 78, 78);
    padding-bottom: 30px;
    margin-top: 30px;
    padding-top: 0px;

    padding-left: 0px;
    padding-right: 0px;
  }

  .map-legend-left {
    /* padding-left: 20px; */
    border-right: solid 1px rgb(53, 53, 53);
    padding-right: 30px;
  }
  .map-legend-bar {
    margin-top: 20px;
    width: 400px;
    display: grid;
    grid-template-columns: repeat(9, 1fr);
  }
  .bar {
    width: 100%;
    /* background: lightgray; */
    height: 20px;
    border: solid 1px #000;
  }
  .bar-text {
    border: none;
    text-align: center;
    font-size: 0.85rem;
    padding-top: 5px;
  }
  @media only screen and (max-width: 600px) {
    .map-legend {
      grid-template-columns: 1fr;
    }
    .map-wrap {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>
