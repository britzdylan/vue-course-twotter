<template>
  <div id="app">
      @{{ user.userName }} - {{fullName}}
      <strong>Followers {{followers}}</strong>
      <button style="width : 75px" @click="followUser">Follow</button>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() { //contains data for the component
    return {
      isLoading: false,
      followers : 0,
      user : {
        id : 1,
        userName : 'britzdm',
        fisrtName : 'Dylan',
        lastName : 'Britz',
        email : 'britzdylan@gmail.com',
        isAdmin : true
      }
    }
  },
  watch : { //do something when data on the  component changes
    followers(newFollowerCount, oldFolowerCount) { //example when the followers change, take two params, new and old data
      if (oldFolowerCount < newFollowerCount) {
        console.log(`${this.user.userName} has gained a follower`);
      }
    }
  },
  computed : { //computed values from the data component , for any complex logic, you should use a computed property. Computed properties are cached based on their reactive dependencies.
    fullName() {
      return `${this.user.fisrtName} ${this.user.lastName}`;
    }
  },
  methods: { //functions mounted on the component
    followUser() {
      this.followers++
    }
  },
  mounted() {// lifecycle methods
    this.followUser();
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  text-align: center;
  align-items: center;
}
</style>
