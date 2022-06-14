<template>
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
export default {
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