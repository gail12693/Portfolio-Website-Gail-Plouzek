<template>
  <div>
    <h2>My GitHub Repositories</h2>
    <div v-if="loading">Loading...</div>
    <div v-else-if="error">{{ error }}</div>
    <ul v-else>
      <li v-for="repo in repositories" :key="repo.id">
        <a :href="repo.html_url" target="_blank">{{ repo.name }}</a>
        <p>{{ repo.description }}</p>
        <p>Language: {{ repo.language }}</p>
        <p>Last updated: {{ new Date(repo.updated_at).toLocaleDateString() }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      repositories: [],
      loading: true,
      error: null,
    };
  },
  async created() {
    try {
      const response = await axios.get('https://api.github.com/users/gail12693/repos');
      this.repositories = response.data;
    } catch (err) {
      this.error = 'Failed to load repositories. Please try again later.';
    } finally {
      this.loading = false;
    }
  },
};
</script>


