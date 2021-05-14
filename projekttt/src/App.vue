<template>
<div id="app">
  <h1>Izberite mesto
    <selector v-on:city='changeCity'/>
  </h1>
  <div class='container'>
   <chart v-bind:data="this.hourlyData"/>
    <today-card :data='this.today'/>
  </div>
  <card-container v-bind:data="this.apiData" />
<div class="graf">
   <chart-teden v-bind:data="this.daily"/>
</div>
 
</div>
</template>

<script>
import cardContainer from './components/CardsContainer.vue'
import Chart from './components/Chart'
import TodayCard from './components/TodayCard'
import Selector from './components/Selector'
import axios from 'axios'
import ChartTeden from './components/Chart -teden.vue'

export default {
  name: 'App',
  components: {
    cardContainer,
    Chart,
    TodayCard,
    Selector,
    ChartTeden,

  },
  data() {
    return {
      data: null,
      today: null,
      apiData: null,
      hourlyData: null,
      daily: null
    }
  },
  created() {     
    this.callApi("Maribor");
   },
   methods: {
     async callApi(value) {
       let koordinate = ""
       if (value == "Maribor")
       {
         koordinate = "lat=46.554650&lon=15.645881"
       }
       else if (value == "Ljubljana")
       {
         koordinate = "lat=46.23092&lon=15.26044"
      
       }
       else {
         koordinate = "lat=49.7475&lon=13.3776"
       }
          this.data = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?${koordinate}&exclude=minutely&appid=8588277e199b1eefa00a01e5ea67b08a`)
          const { daily, hourly, current } = this.data.data;
          this.today = current;
          daily.shift()
          this.daily = daily
          this.apiData = Array(daily);
          this.hourlyData = hourly.splice(0,hourly.length/2);
          console.log(this.hourlyData);
           console.log(this.apiData);
           console.log(this.daily)
     },
     changeCity(value) {
      this.callApi(value);
     }
   }
}
</script>

<style>
* {
    margin:0 auto;
}

.container {
  width: 70%;
  display: flex;
  align-content: space-between;
}

h1 {
  font-size: 55px;
  margin-bottom: 20px;
  color: #272727;
}

.wawes{
  position: absolute;
  bottom: 0;
  left: 0;
  z-index: -1;

}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ADADAD;
  height: 100%;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.custom-select {
  position: relative;
  font-family: Arial;
}

.custom-select select {
  display: none; /*hide original SELECT element: */
}

.select-selected {
  background-color: DodgerBlue;
}

/* Style the arrow inside the select element: */
.select-selected:after {
  position: absolute;
  content: "";
  top: 14px;
  right: 10px;
  width: 0;
  height: 0;
  border: 6px solid transparent;
  border-color: #fff transparent transparent transparent;
}

/* Point the arrow upwards when the select box is open (active): */
.select-selected.select-arrow-active:after {
  border-color: transparent transparent #fff transparent;
  top: 7px;
}

/* style the items (options), including the selected item: */
.select-items div,.select-selected {
  color: #ffffff;
  padding: 8px 16px;
  border: 1px solid transparent;
  border-color: transparent transparent rgba(0, 0, 0, 0.1) transparent;
  cursor: pointer;
}

/* Style items (options): */
.select-items {
  position: absolute;
  background-color: DodgerBlue;
  top: 100%;
  left: 0;
  right: 0;
  z-index: 99;
}

/* Hide the items when the select box is closed: */
.select-hide {
  display: none;
}

.select-items div:hover, .same-as-selected {
  background-color: rgba(0, 0, 0, 0.1);
}
</style>
