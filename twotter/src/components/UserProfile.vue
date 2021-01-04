<template>
<div class="user-profile">
    <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{ user.userName }}</h1>
        <!-- condition v-if do something when user is admin aka true -->
        <div v-if="user.isAdmin" class="user-profile_admin-badge"> 
            <p>Admin</p>
        </div>
        <!-- else do this -->
        <div v-else class="user-profile_admin-badge">
            <p>not Admin</p>
        </div>
        <div class="user-profile_follower-count">
            <strong>Followers: </strong> {{followers}}
        </div>
    </div>
    <div class="user-profile__twoots-wrapper">
        <!-- create a list with v-for, render everything including the outer div not just the children. @ = call the function favourite when the cild function is triggered -->
        <TwootItem 
        class="user-profile_twoot" 
        :key="twoot.id" 
        v-for="twoot in user.twoots" 
        :username="user.userName" 
        :twoot="twoot" 
        @favourite="toggleFavourite"/>
    </div>
</div>
</template>

<script>
import TwootItem from './TwootItem'


export default {
  name: 'UserProfile',
  components : { TwootItem },
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
        isAdmin : false,
        twoots : [
            { id: 1, content : 'Twotter is amazing!'},
            { id: 2, content : 'Twotter is amazing, again!'}
        ]
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
    },
    toggleFavourite(id) {
        console.log('favourited the tweet ', id);
    }
  },
  mounted() {// lifecycle methods
    this.followUser();
  }
}

</script>
<style>
    .user-profile {
        display: grid;
        grid-template-columns: 1fr 3fr;
        width : 100%;
        padding: 50px 5%;
 
    }
    .user-profile__user-panel {
        display: flex;
        flex-direction: column;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #DFE3E8;
        margin-right: 50px;
    }

    h1 {
        margin: 0;
    }

    .user-profile_admin-badge {
        border-radius: 2px;
        background-color: black;
        margin-right: auto;
        color : white;
        padding :  0 10px;
    }

    .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
  
</style>
