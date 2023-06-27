<template>
    <div>
      <form @submit.prevent="search">
        <input type="text" v-model="searchTerm" placeholder="Enter your search term">
        <button type="submit">Search</button>
      </form>

      <div>
        <ul v-if="results.length > 0">
            <table class="style table">
                <tr class="style">
                    <th class="style">ID</th>
                    <th class="style">Title</th>
                    <th class="style">Author</th>
                </tr>
                <tr class="style" v-for="(result, index) in results" :key="index">
                    <td class="style">{{ result.id }}</td>
                    <td class="style">{{ result.title }}</td>
                    <td class="style">{{ result.author }}</td>
                </tr>
            </table>
        </ul>
        <p v-else>No results found.</p>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  export default {
    data() {
      return {
        searchTerm: '',
        results: []
      };
    },
    methods: {
      search() {
        axios.get('http://localhost:3000/posts', {
          params: {
            title: this.searchTerm
          }
        })
        .then(response => {
          this.results = response.data;
        })
        .catch(error => {
          console.error(error);
        });
      }
    }
  };
  </script>
  