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
<div id="app">
  <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/28963/vue-post-photo.jpg" class="main-photo">
  <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/28963/vue-main-profile.jpg" class="main-profile">
  <div class="main-info">
    <span class="name">Julianne Delfina</span> 
    <h3>"It's lovely after it rains"</h3>
  </div>
  <hr>
  
  <ul>
    <li v-for="comment in comments" :key="comment">
      {{ comment }}
    </li>
  </ul>
  
  <input
    @keyup.enter="addComment"
    v-model="newComment"
    placeholder="Add a comment"
  />
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
  },
   data() {
    return {
      newComment: '',
      comments: [
        'Looks great Julianne!',
        'I love the sea',
        'Where are you at?'
      ]
    }
  },
  methods: {
    addComment() {
      this.comments.push(this.newComment)
      this.newComment = ''
    }
  }
}
</script>
