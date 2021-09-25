<template>
  <header class="header">
    <a class="header__logo" href="./">devfinder</a>
    <div class="header__theme">
      <input type="checkbox" id="theme" class='theme' v-model="darkMode"/>
      <label for="theme">
        {{ darkMode ? 'light' : 'dark' }}
        <img :src="require(`@/assets/images/icon-${darkMode ? 'sun' : 'moon'}.svg`)">
      </label>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      darkMode: false
    }
  },
  mounted() {
    let theme = localStorage.getItem("theme");

    if (theme === 'dark') {
      document.body.className = 'dark'
      this.darkMode = true
    } else {
      document.body.className = ''
      this.darkMode = false
    }
  },
  watch: {
    darkMode(){
      if (this.darkMode) {
        localStorage.setItem("theme", 'dark');
        document.body.className = 'dark'
      } else {
        localStorage.setItem("theme", '');
        document.body.className = ''
      }
    }
  }
}
</script>

<style lang="sass">
.header
  display: flex
  align-items: center
  justify-content: space-between
  margin-top: 3.1rem
  @media screen and (min-width: 768px)
    margin-top: 14rem
  @media screen and (min-width: 992px)
    margin-top: 14.4rem
  &__logo
    color: var(--col-text-dark)
    font-size: 2.6rem
    font-weight: bold
  &__theme
    display: flex
    align-items: center
    & input[type="checkbox"]
      display: none
    & label
      color: var(--col-text)
      cursor: pointer
      display: flex
      align-items: center
      font-size: 1.3rem
      font-weight: bold
      letter-spacing: 2.5px
      text-transform: uppercase
      & img
        margin-left: 1.6rem
</style>