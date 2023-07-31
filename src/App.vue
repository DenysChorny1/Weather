<script>
import axiox from 'axios'

  export default {
    data() {
      return {
        city: '',
        error: '',
        info: null
      }
    },
    computed: {
      cityName() {
        return this.city
      },
      showTemp() {
        return 'Temp: ' + this.info.main.temp
      },
      showFeelsLike() {
        return 'Temp feel like: ' + this.info.main.feels_like
      },
      showMinTemp() {
        return 'Min temp: ' + this.info.main.temp_min
      },
      showMaxTemp() {
        return 'Min temp: ' + this.info.main.temp_max
      }
    },
    methods: {
      gerWeather() {
        if(this.city.trim().length < 2){
          this.error = "Error"
          return false
        }
        this.error = ''
        axiox.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=b5d5d3df2477e5656a9bdc6e3e6a1488`)
        .then(res => (this.info = res.data))
        console.log(this.info)
      }
    }
  }
</script>

<template>
  <div class="wrapper">
    <h1>Weather</h1>
    <p>{{ city == '' ? 'Your city' : cityName }}</p>
    <input type="text" placeholder="City" v-model="city">
    <button v-if="city !=''" @click="gerWeather()">Get weather</button>
    <button disabled v-else>City?</button>
    <p class="error">{{ error }}</p>
    <div v-if="info != null">
      <p>{{ showTemp }}</p>
      <p>{{ showFeelsLike }}</p>
      <p>{{ showMinTemp }}</p>
      <p>{{ showMaxTemp }}</p>
    </div>
  </div>
</template>

<style scoped>
.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background-color: rgb(50, 31, 48);
  padding: 20px;
  text-align: center;
  color: #fff;
}
.wrapper h1{
  margin-top: 50px;
}
.wrapper input{
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  margin-top: 30px;
  font-size: 14px;
  padding: 5px 10px;
  color: #fff;
  outline: none;
}
.wrapper input:focus{
  border-bottom-color: #6e2d7d;
}
.wrapper button{
  background: #e3dc4d;
  color: #fff;
  border: 2px solid #e3dc4d;
  padding: 10px 15px;
  margin-left: 20px;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover{
  border: 2px solid #b99935;
  transform: scale(1.1) translateY(-5px);
}
.error{
  color: red;
}
</style>
