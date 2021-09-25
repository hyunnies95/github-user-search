<template>
  <form class="search" v-on:submit.prevent>
    <img class="search__icon" src="@/assets/images/icon-search.svg" alt="search">
    <input type="text" placeholder="Search GitHub username..." v-model="username">
    <p v-if="error" class="error">No results</p>
    <button @click="search(username)" type="submit">Search</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      user: {},
      error: false
    }
  },
  mounted() {
    this.search('octocat')
  },
  methods: {
    search(username) {
      let api = 'https://api.github.com/users/' + username

      this.axios.get(api)
        .then((response) => {
          this.user = response.data
          this.error = false
          this.$emit('search', this.user)
        })
        .catch((error) => {
          console.log('No results' + error)
          this.error = true
        })
    }
  }
}
</script>

<style lang="sass">
.search
  background-color: var(--col-bg)
  border-radius: 1.5rem
  box-shadow: 0px 5px 15px var(--col-shadow)
  display: flex
  align-items: center
  position: relative
  padding: 0.65rem 0.7rem 0.75rem 1.6rem
  margin-top: 3.6rem
  height: 6rem
  @media screen and (min-width: 768px)
    padding: 0.95rem 1rem 0.95rem 3.2rem
    height: 6.9rem
  &__icon
    width: 2rem
    @media screen and (min-width: 768px)
      width: 2.4rem
  & input
    color: var(--col-text-dark)
    font-size: 1.3rem
    margin: 0 2.4rem 0 0.9rem
    width: 100%
    @media screen and (min-width: 768px)
      font-size: 1.8rem
      margin: 0 2.4rem
    &::placeholder
      color: var(--col-text)
  & button
    color: var(--col-white)
    background-color: var(--col-accent)
    border-radius: 1rem
    font-size: 1.4rem
    font-weight: bold
    margin-left: auto
    height: 4.6rem
    min-width: 8.4rem
    transition: $transition background-color
    @media screen and (min-width: 768px)
      font-size: 1.6rem
      height: 5rem
      min-width: 10.6rem
    &:hover
      background-color: var(--col-accent-hover)
</style>