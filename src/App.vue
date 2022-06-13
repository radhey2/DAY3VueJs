<template>
  <div id="app" >
  <div @mousemove="xCoordinate" :style="{ backgroundColor: `hsl(${x}, 80%, 50%)` }" class="box">
    <p>
      <button v-on:click="increment(5)">+ 5</button> 
      {{ counter }} 
      <button @click="decrement(5)">- 5</button>
    </p>
    <p>Pixels across: {{ x }}</p>
  </div>
</div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
  	return {
  		counter: 0,
      x: 0
  	}
  },
  methods: {
	  increment(num) {
	  	this.counter+= num;
	  },
    decrement(num) {
	  	this.counter-= num;
	  },
    xCoordinate(e) {
      this.x = e.clientX;
    }
  }
}
</script>
