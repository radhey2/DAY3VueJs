<template>
    <div id="app">
  <section>
    <h1>🍺 Make yourself some Punk Beers 🍻</h1>
    <div v-if="!beers.length" class="loading">Loading...</div>
    <div v-for="beer in beers" :key="beer" class="beer-contain" >
      <div class="beer-img">
        <img :src="beer.img" height="350" />
      </div>
      <div class="beer-info">
        <h2>{{ beer.name }}</h2>
        <p class="bright">{{ beer.tagline }}</p>
        <p><span class="bright">Description:</span> {{ beer.desc }}</p>
        <p><span class="bright">Tips:</span> {{ beer.tips }}</p>
        <h3 class="bright">Food Pairings</h3>
        <ul>
          <li v-for="item in beer.food" :key="item">
            {{ item }}
          </li>
        </ul>
      </div>
    </div>
  </section>
</div>
</template>

<script>
import axios from 'axios';
export default {
     data() {
    return {
      bottom: false,
      beers: []
    };
  },
  watch: {
    bottom(newValue) {
      if (newValue) {
        this.addBeer();
      }
    }
  },
  created() {
    window.addEventListener("scroll", () => {
      this.bottom = this.bottomVisible();
    });
    this.addBeer();
  },
  methods: {
    bottomVisible() {
      const scrollY = window.scrollY;
      const visible = document.documentElement.clientHeight;
      const pageHeight = document.documentElement.scrollHeight;
      const bottomOfPage = visible + scrollY >= pageHeight;
      return bottomOfPage || pageHeight < visible;
    },
    addBeer() {
      axios.get("https://api.punkapi.com/v2/beers/random").then((response) => {
        let api = response.data[0];
        let apiInfo = {
          name: api.name,
          desc: api.description,
          img: api.image_url,
          tips: api.brewers_tips,
          tagline: api.tagline,
          food: api.food_pairing
        };
        this.beers.push(apiInfo);
        if (this.bottomVisible()) {
          this.addBeer();
        }
      });
    }
  }
}
</script>