<script>
import axios from 'axios'

  export default {
    data(){
      return {
        city: "",
        error: "",
        info: null
      }
    },
    computed: {
      cityName(){
        return '\"' + city + '\"'
      }
    },
    methods: {
      getWeather(){
          if(this.city.trim().length < 2){
            this.error = "Too shot city name :(("
            return false
          }

          this.error = ""

          
          axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=0396885de5299fad7a5f25d3b7840ea8`)
          .then(res => (this.info = res.data.main))    
          
      }
    }     
    
  }
</script>

<template>
  <div class='wrapper'>
    <h1>Погодное приложение</h1>
    <p>Узнать погоду в {{city == "" ? "вашем городе" : '\"' + city + '\"'}}</p>
    <input type='text' v-on:input="this.city=$event.target.value" placeholder="Введите город">
    <button v-if="city!=''" @click="getWeather()">Получить погоду</button>
    <button v-else disable>Введите город</button> 
    <p class="error">{{ error }}</p>
    <div v-show="info != null">
       <p>Текущая температура: {{ info.temp }}`C</p>
       <p>Ощущается как: {{ info.feels_like }}`C</p>
       <p>Минимальная температура: {{ info.temp_min }}`C</p>
       <p>Максимальная температура: {{ info.temp_max }}`C</p>
    </div>
  </div>  
</template>

<style scoped>
.error{
    color: #d03939;
}
.wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    background: #1f0f24;
    padding: 20px;
    text-align: center;
    color: #fff;
}
.wrapper h1 {
    margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input{
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5px 8px;
    outline: none; 
}
.wrapper input:focus{
  border-bottom-color: #6e2d7d;
}
.wrapper button:disabled{
    background: #746027;
    cursor: not-allowed;
}
.wrapper button{
    background: #e3bc4b;
    color: #fff;
    border-radius: 10px;
    border: 2px solid #b99935;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 500ms ease;
    padding: 10px 15px;
}

.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}

</style>
