<template>
  <div class="zip">
      <div class="jumbotron contain">
        <h4>Enter Zip Code</h4>
        <form @submit.prevent="getLocation"> 
          <input v-model="current">
        </form>
      </div>
      <div class="contain">
        
        <p class="alert alert-danger" role="alert" v-if="error">{{error}}</p>
      <div v-for="place in places" :key="place.state">
        <ul class="list-group">
          <li class="list-group-item active">{{place['place name']}}</li>
          <li class="list-group-item">{{place.state}}</li>
          <li class="list-group-item">{{place['state abbreviation']}}</li>
          <li class="list-group-item">{{place.latitude}}</li>
          <li class="list-group-item">{{place.longitude}}</li>
        </ul>
      </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'zip',
  data () {
    return {
      current: '',
      error: '',
      places:[],
    }
  },
  methods: {
    getLocation: function(){
      this.$http.get('http://api.zippopotam.us/us/'+ this.current)
      .then(response=>{
        // this.places='';
        // this.error = '';
        this.places = response.data.places;
        console.log(response)
        
      })
      .catch(() => {
        this.error = 'Please enter a valid Zip code'
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .contain{
    width: 40%;
    margin-left: 25%;
    margin-top: 10px;
}
</style>
