<template>
  <div id="home">
    <h1>This is the home page</h1>
    <br>
    <h2>👨🏻‍🎤 Here are our random users:</h2>
    <br>

    <div v-if="resultsArray">
      <div class="flex">
        <div v-for="(user, i) in resultsArray" :key="i">
          <!-- Can't really use router params since the API doesn't support individual
          user IDs, so I used router-link params -->
          <router-link class="router-link" :to="{ path:'/user', query: 
          { pfp:user.picture.large, 
            title: user.name.title, 
            firstName: user.name.first,
            lastName: user.name.last,
            dob: user.dob.date,
            por: user.location.city,
            email: user.email,
            phone: user.phone }}">
            <div class="flex-card">
              <div class="card-img" :style="`background: url(${user.picture.medium})`"></div>
              <div class="card-text">
                {{ `${user.name.title} ${user.name.first}` }} <br>
                {{ user.name.last }}
              </div>
            </div>
            </router-link>
        </div>

      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Home',

  data(){
    return {
      resultsArray: undefined,
      // If we want to generate the same users every time, API documentation states that we need
      // to add the 'seed' param eg '&seed=asf71nabfcdb099ad'
      API_URL: "https://randomuser.me/api/?results=200&exc=login",
    }
  },

  mounted(){
    this.axios.get(this.API_URL)
    .then((response) => {
      // api doesn't have parameters for age and timezone so we have to filter results
      // client-side; I decided to take 200 results with the assumption that I will have
      // 15 candidates that pass the parameters
      // this is obviously not the best idea for production but if it were in production,
      // I would have to catch the error if the final array's length finalArray.length() < 15
      let myArray = response.data;
      const filteredArray = myArray.results.filter(result => 
        // array needs to be filtered
        // first filter is if the timezone is above -1:00
        // second and third filter is if the timezone is below +1:00
        // fourth filter is if the age is above 18
        ((parseInt(result.location.timezone.offset.split(":")[0]) >= -1) && 
        (parseInt(result.location.timezone.offset.split(":")[0]) <= 1) && 
        (parseInt(result.location.timezone.offset.split(":")[0]) == 1 ? ( parseInt(result.location.timezone.offset.split(":")[1]) == 0 ? true : false ) : true) && 
        (result.dob.age >= 18)));
      this.resultsArray = filteredArray.slice(0, 15);

      // console.log(this.resultsArray);
    });
  }
}
</script>

<style scoped>
.flex {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.flex-card {
  width: calc((85vw / 3) - 30px);
  margin: 15px;
  border-radius: 5px;
  background-color: #f1f1f1;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
  overflow: hidden;
  height: 150px;
  display: flex;
  flex-direction: row;
  align-items: center;
}

.flex-card:hover {
  background-color: #dadada;
  box-shadow: 2px 2px 15px rgba(0, 0, 0, 0.7);
}

.card-img {
  width: 40%;
  height: 100%;
  background-position: center !important;
  background-size: cover !important;
  background-repeat: no-repeat !important;
}

.card-text {
  margin: 10px;
  word-wrap: break-word;
}

.router-link {
  color: #353535;
}

@media screen and (max-width: 768px) {
  .flex {
    flex-direction: column;
  }

  .flex-card {
    width: 100%;
    height: 200px;
    margin-left: 0;
    margin-right: 0;
  }

  .card-img {
    height: 100%;
  }
}
</style>