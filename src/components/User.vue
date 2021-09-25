<template>
  <section class="user">

    <div class="user__info">
      <div class="user__avatar">
        <img :src="user.avatar_url" :alt="user.name">
      </div>
      <div class="user__names">
        <div>
          <h1 class="user__name">{{ user.name }}</h1>
          <h3 class="user__nickname">@{{ user.login }}</h3>
        </div>
        <p class="user__joined">
          Joined {{day + ' ' + month + ' ' + year}}
        </p>
      </div>
      <p class="user__bio" v-if="user.bio">{{ user.bio }}</p>
      <p class="user__bio" v-else>This profile has no bio</p>  
    </div>

    <ul class="user__data">
      <li>
        <h4>Repos</h4>
        <h2>{{ user.public_repos }}</h2>
      </li>
      <li>
        <h4>Followers</h4>
        <h2>{{ user.followers }}</h2>
      </li>
      <li>
        <h4>Following</h4>
        <h2>{{ user.following }}</h2>
      </li>
    </ul>

    <ul class="user__contacts">
      <li :class="{ disabled: user.location === null }">
        <img src="@/assets/images/icon-location.svg" alt="location"> 
        <p>{{ user.location || 'Not Available'}}</p>
      </li>
      <li :class="{ disabled: user.html_url === null }">
        <img src="@/assets/images/icon-website.svg" alt="website"> 
        <p><a :href="user.html_url" target="_blank" rel="noopener noreferrer">{{ user.html_url }}</a></p>
      </li>
      <li :class="{ disabled: user.twitter_username === null }">
        <img src="@/assets/images/icon-twitter.svg" alt="twitter"> 
        <p>{{ user.twitter_username || 'Not Available'}}</p>
      </li>
      <li :class="{ disabled: user.company === null }">
        <img src="@/assets/images/icon-company.svg" alt="company"> 
        <p>{{ user.company || 'Not Available'}}</p>
      </li>
    </ul>

  </section>
</template>

<script>
export default {
  props: ['user'],
  computed: {
    joined() {
      return this.user.created_at.split('T').shift().split('-')
    },
    day() {
      return this.joined[2]
    },
    month() {
      const months = [ 'Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec' ]
      return months[this.joined[1] - 1] 
    },
    year() {
      return this.joined[0]
    }
  }
}
</script>

<style lang="sass">
.user
  background-color: var(--col-bg)
  border-radius: 1.5rem
  box-shadow: 0px 5px 15px var(--col-shadow)
  padding: 3.2rem 2.4rem 4.8rem
  margin-top: 1.6rem
  @media screen and (min-width: 768px)
    grid-template-columns: 11.7rem 1fr
    padding: 4rem
    margin-top: 2.4rem
  @media screen and (min-width: 992px)
    padding: 4.8rem
  &__info
    display: grid
    grid-template-columns: 7rem 1fr
    column-gap: 1.9rem
    gap: 3.3rem
    @media screen and (min-width: 768px)
      grid-template-columns: 11.7rem 1fr
      column-gap: 4.1rem
      gap: 2.4rem
    @media screen and (min-width: 992px)
      grid-template-rows: 5.7rem 1fr
      column-gap: 3.7rem
  &__avatar
    width: 100%
    @media screen and (min-width: 992px)
      grid-column: 1 / 2
      grid-row: 1 / 3
    & img
      border-radius: 50%
      width: 100%
  &__names
    @media screen and (min-width: 992px)
      display: flex
      justify-content: space-between
      margin-top: -0.3rem
    & p
      color: var(--col-text-secondary)
      font-size: 1.3rem
      @media screen and (min-width: 768px)
        font-size: 1.5rem
  &__bio
    grid-column: 1 / 3
    @media screen and (min-width: 992px)
      grid-column: 2 / 3
  &__data
    background-color: var(--col-bg-app)
    border-radius: 1rem
    grid-column: 1 / 3
    display: flex
    align-items: center
    justify-content: space-around
    text-align: center
    padding: 1.9rem 2.8rem
    margin: 2.3rem 0 2.4rem
    height: 8.5rem
    @media screen and (min-width: 768px)
      justify-content: start
      column-gap: 25%
      text-align: left
      padding: 1.6rem 3.2rem
      margin: 3.2rem 0 3rem
    @media screen and (min-width: 992px)
      grid-column: 2 / 3
      margin: 3.2rem 0 3.7rem
  &__contacts
    display: grid
    gap: 1.6rem
    grid-column: 1 / 3
    @media screen and (min-width: 768px)
      grid-template-columns: repeat(2, 1fr)
      gap: 1.9rem
    @media screen and (min-width: 992px)
      grid-column: 2 / 3
    & li
      display: grid
      align-items: center
      grid-template-columns: 3.3rem 1fr
      & a:hover
        text-decoration: underline
      &.disabled
        opacity: 0.5
</style>