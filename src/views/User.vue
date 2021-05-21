<template>
  <div id="user">

    <router-link class="router-link" to="/"><span class="left-arrow">&lt;</span> Back to Homepage</router-link>
    <br><br>

    <div class="user-info">
      <img class="user-pfp" :src="userProfilePicture" alt="User's profile picture">

      <h3>{{ userTitle + " " + userFirstName + " " + userLastName }}</h3>
      <p>{{ "Date of birth: " + userDateOfBirth }}</p>
      <p>{{ "Place of residence: " + userResidence }}</p>
      <p>{{ "Email: " + userEmail }}</p>
      <p>{{ "Phone: " + userPhone }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "User",

  data(){
    return {
      userProfilePicture: undefined,
      userTitle: undefined,
      userFirstName: undefined,
      userLastName: undefined,
      userDateOfBirth: undefined,
      userResidence: undefined,
      userEmail: undefined,
      userPhone: undefined
    }
  },

  mounted(){
    this.userProfilePicture = this.$route.query.pfp;
    this.userTitle = this.$route.query.title;
    this.userFirstName = this.$route.query.firstName;
    this.userLastName = this.$route.query.lastName;
    const date = this.$route.query.dob;
    this.userDateOfBirth = date.split("T")[0].split("-")[2] + "." + date.split("T")[0].split("-")[1] + "." + date.split("T")[0].split("-")[0] + ".";
    this.userResidence = this.$route.query.por;
    this.userEmail = this.$route.query.email;
    this.userPhone = this.$route.query.phone;
  }
}
</script>

<style scoped>
.router-link {
  text-decoration: none;
  color: #353535;
  font-size: 1.2rem;
}

.left-arrow {
  border: 1px solid #353535;
  border-radius: 50%;
  padding: 1px 7px;
}

.user-pfp {
  float: left;
  margin-right: 10px;
  margin-bottom: 10px;
}

@media screen and (max-width: 768px) {
  .user-pfp {
    width: 100%;
    margin-bottom: 20px;
  }

  .user-info {
    text-align: center;
  }

  h3 {
    font-size: 1.8rem;
  }

  p {
    font-size: 1.4rem;
  }
}
</style>