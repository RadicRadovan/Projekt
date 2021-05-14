<template>
  <div class='danes'>
      <div class='container'>
        <div class='leva'>
          <h3>Danes</h3>
          <h3>{{(new Date()).toISOString().slice(0, 10).replace(/-/g, "-").replace("T", " ") }}</h3>
        </div>
        <h4>{{ Math.round(data.temp-273)+'°C' }}</h4>
      </div>
      <div class='container'>
        <div class='detaily'>
            <p>{{'Občutek: '+Math.round(data.feels_like-273)+'°C'}}</p>
            <p>{{'Pritisak: '+data.pressure+' hPa'}}</p>
            <p>{{'Hitrost vetra/zraka: '+data.wind_speed}}</p>
        </div>
       
      </div>
      
  </div>
</template>

<script>
export default {
 name: 'Danes',
 props: ['data'],
 
 
}
</script>

<style scoped>
.danes {
  padding-top: 2px;
  width: 30%;
  height: 250px;
  background-color: #333538;
  border-top: 5px solid #FFBE00;
  border-radius: 5px;
}
img {
    height: 80px;
    width: 80px;
}

h4 {
  font-size: 50px;
}

.sun-container {
  margin-top: 5px;
  display: flex;
  align-content: space-between;
}

.sunrise > img {
  height: 60px;
  width: 60px;
}

.sunset > img {
  height: 60px;
  width: 60px;
}
</style>