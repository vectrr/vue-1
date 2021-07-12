<template>
  <Layout>
    <h2 class="mb-8 text-4xl font-bold text-center capitalize">
      Home page
    </h2>
    <mlist :posts="posts" />
  </Layout>
</template>

<script>
// import Layout from "./Layout.vue"
// import NewsFilter from "./components/NewsFilter.vue"
import mlist from "./list.vue"
import axios from "axios"

// import data from "./posts.json"

export default {
  components: {
    // Layout,
    // NewsFilter,
    mlist,
  },
  

  data() {
    return {
      posts: [],
    }
  },
  methods: {
    // Helper function for extracting a nested image object
   
    async fetchNews() {
      try {
        const url = "https://ti-react-test.herokuapp.com/users"
        const response = await axios.get(url)
          console.log("Server Error:", response.data)
        const results = response.data
        this.posts = results.map(post => ({
          id: post.id,
          name: post.name,
          occupation: post.occupation,
          email: post.email,
          bio: post.bio,
          created_at: post.created_at,
          updated_at: post.updated_at
         
        }))
      } catch (err) {
        if (err.response) {
          // client received an error response (5xx, 4xx)
          console.log("Server Error:", err)
        } else if (err.request) {
          // client never received a response, or request never left
          console.log("Network Error:", err)
        } else {
          console.log("Client Error:", err)
        }
      }
    },
  },
  mounted() {
    this.fetchNews()
  },

}
</script>