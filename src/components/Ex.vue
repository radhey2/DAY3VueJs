<template>
    <div id="app">
  <div class="contain">
    <h2>Blog Posts</h2>

    <div class="new">
      <h3>Add a New Post</h3>
      <form>
        <input v-model="newTitle" placeholder="title" required/>
        <input v-model="newAuthor" placeholder="author name" required/>
        <select v-model="newLabel" required>
        <option disabled value="">Add a New label</option>
        <option>science</option>
        <option>math</option>
        <option>poetry</option>
        <option>history</option>
      </select>
        <button type="submit">Add New Blog Post</button>
      </form>
    </div>

    <select v-model="selected">
      <option disabled value="">Filter with a label</option>
      <option>science</option>
      <option>math</option>
      <option>poetry</option>
      <option>history</option>
    </select>

    <div v-for="post in posts" :key="post.title" class="post">
      <span class="label">{{ post.label }}</span>
      <p>{{ post.title }}</p>
      <small>{{ post.author }}</small>
    </div>
  </div>
</div>
</template>

<script>
export default {
    name: 'App',
    data() {
    return {
      selected: '',
      posts: [
        {
          author: '@vFitzgerald',
          title: 'Quod Ducimus Omnis',
          label: 'science'
        },
        {
          author: '@mPalmer',
          title: 'Vero Eius Laboriosam Ex Repudiandae',
          label: 'math'
        },
        {
          author: '@mDean',
          title: 'Magnam Odit',
          label: 'science'
        },
        {
          author: '@tCole',
          title: 'Velit Mollitia Voluptates Assumenda',
          label: 'science'
        },
        {
          author: '@jCooper',
          title: 'Eum Commodi Cupiditate',
          label: 'poetry'
        },
        {
          author: '@lLamb',
          title: 'Amet',
          label: 'history'
        },
        {
          author: '@fMartin',
          title: 'Voluptatem Fuga Cum Asperiores Error',
          label: 'science'
        },
        {
          author: '@eHayes',
          title: 'Ipsa Consectetur Rerum Repellat Quia',
          label: 'math'
        },
        {
          author: '@cCollier',
          title: 'Dolor Nihil Delectus',
          label: 'science'
        },
        {
          author: '@cBenson',
          title: 'Labore Ipsum Ad Pariatur',
          label: 'poetry'
        }
      ],
      newTitle: '',
      newAuthor: '',
      newLabel: '',
    }
  }
}
</script>