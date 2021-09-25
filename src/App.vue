<template>
<div class="container">
  <Header />
  <Search @search="onSearch" />
  <User :user="user" />
</div>
</template>

<script>
import Header from './components/Header.vue'
import Search from './components/Search.vue'
import User   from './components/User.vue'

export default {
  name: 'App',
  components: {
    Header,
    Search,
    User
  },
  data() {
    return {
      user: []
    }
  },
  methods: {
    onSearch(user) {
      this.user = user
    }
  },
}
</script>