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
<div id="app">
  <form @submit.prevent="submitForm">
    <div>
      <label for="name">Name:</label><br>
      <input id="name" type="text" v-model="name" required/>
    </div>
    <div>
      <label for="email">Email:</label><br>
      <input id="email" type="email" v-model="email" required/>
    </div>
    <div>
      <label for="caps">HOW DO I TURN OFF CAPS LOCK:</label><br>
      <textarea id="caps" v-model="caps" required></textarea>
    </div>
    <button :class="[name ? activeClass : '']" type="submit">Submit</button>
    <div>
      <h3>Response from server:</h3>
      <pre>{{ response }}</pre>
    </div>
  </form>
</div>
<div id="app">
  <h3>Sort titles by: 
    <button @click="sortLowest">Lowest Rated</button>
    <button @click="sortHighest">Highest Rated</button>
  </h3>
  <table>
    <thead>
      <tr>
        <th v-for="key in columns">
          {{ key }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="entry in ratingsInfo">
        <td v-for="key in columns">
          {{entry[key]}}
        </td>
      </tr>
    <tbody>
  </table>
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
  },
   data() {
    return {
      name: '',
      email: '',
      caps: '',
      response: '',
      activeClass: 'active'
    }
  },
  methods: {
    submitForm() {
      axios.post('//jsonplaceholder.typicode.com/posts', {
        name: this.name,
        email: this.email,
        caps: this.caps
      }).then(response => {
        this.response = JSON.stringify(response, null, 2)
      }).catch(error => {
        this.response = 'Error: ' + error.response.status
      })
    }
  },
   data() {
    return {
      columns: ["title", "rating"],
      ratingsInfo: [
        { title: `White Chicks`, rating: 82 },
        { title: `Grey's Anatomy`, rating: 98 },
        { title: `Prison Break`, rating: 98 },
        { title: `How I Met Your Mother`, rating: 94 },
        { title: `Supernatural`, rating: 95 },
        { title: `Breaking Bad`, rating: 97 },
        { title: `The Vampire Diaries`, rating: 91 },
        { title: `The Walking Dead`, rating: 98 },
        { title: `Pretty Little Liars`, rating: 96 },
        { title: `Once Upon a Time`, rating: 98 },
        { title: `Sherlock`, rating: 95 },
        { title: `Death Note`, rating: 77 },
        { title: `Naruto`, rating: 88 },
        { title: `Arrow`, rating: 96 },
        { title: `Black Mirror`, rating: 80 },
        { title: `The Originals`, rating: 74 },
        { title: `The 100`, rating: 97 },
        { title: `Masha and the Bear`, rating: 81 },
        { title: `Hunter X Hunter`, rating: 57 },
        { title: `Marvel's Luke Cage`, rating: 95 },
        { title: `Marvel's Iron Fist`, rating: 98 }
      ]
    }
  },
  methods: {
    sortLowest() {
      this.ratingsInfo.sort((a, b) => a.rating > b.rating ? 1 : -1);
    },
    sortHighest() {
      this.ratingsInfo.sort((a, b) => a.rating < b.rating ? 1 : -1);
    }
  }
}
</script>
