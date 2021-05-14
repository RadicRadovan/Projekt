<template>
  <div class='card'>
      <h2>{{ Math.round(data.temp.day-273)+'°C' }}</h2>
     
      <h5>{{ new Date(data.dt * 1000).toLocaleString("default", { weekday: "long" }) }}</h5>
 
      
  </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['data'],
  

}
</script>

<style scoped>
.card {
    height: 130px;
    background-color: #333538;
    width: 10%;
    border-top: 5px solid #FFBE00;
    border-radius: 5px;
    transition: all .1s ease-in-out;
}

img {
    width:70px;
    height:70px;
}

.card:hover {
  transform: scale(1.2);
}
</style>