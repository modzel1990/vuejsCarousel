<template>
  <div class="info">
    <!-- Ideally we would do checks for specific values if they exist, as if we would pass empty values we will
    encounter errors -->
    <ul class="list-unstyled">
      <li>
        Name : {{ user.name }}
      </li>
      <li>
        Surname: {{ user.surname }}
      </li>
      <li>
        Address: {{ user.address }}
      </li>
      <li>
        Profile: <img v-if="getImage(user.profile)" :src="require(`@/assets/${user.profile}`)"
                      class="d-block w-25 img-fluid img"
                      alt="..."
                  >
      </li>
    </ul>
    <router-link :to="{ name: 'Home' }"><button class="btn btn-outline-dark d-inline w-25 m-2 btn-rounded">Back</button></router-link>
  </div>
</template>

<script>

export default {
  name: 'Info',
  props: ['user'],
  methods: {
    getImage (fileName) {
      try {
        return require(`@/assets/${fileName}`)
      } catch (e) {
        return false
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .img {
    display: block;
    width: 100%;
    margin: auto;
  }
</style>
