<template>
<div class='container'>
  <card v-for="item in data[0]" :key='item' v-bind:data="item"/>
</div>
</template>

<script>
import Card from './Card'

export default {
    name: 'CardsContainer',
    components: {
        Card,
    },
    props: ['data'],    
}
</script>

<style scoped>
.container {
  display: flex;
  align-content: space-between;
  width: 70%;
  margin-top: 10px;
}
</style>