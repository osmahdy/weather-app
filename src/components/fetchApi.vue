<template>
    <div class="total">
        <input type="input" placeholder="Search..." class="search" @keydown="apifetch" v-model="this.value" ref="input">
            <div class="main" ref="main">
                <div class="weeklyForcast">
                    <div class="top" ref="location">
                        <p>{{ this.location.country + '-' +  this.location.name}}</p>
                        <p>{{ this.date}}</p>
                    </div>
                    <mainWedgit
                    :temp="this.current.temp_c" 
                    :hum="this.current.humidity"
                    :wind="this.current.wind_mph"
                    :status="this.condition.text"
                    ></mainWedgit>
                    <div class="bottom">
                        <cardsComp class="card"
                         v-for="(day,index) in this.forecastday" :key="index"
                        :day="getDayName(day.date)" 
                        :temp="day.day.avgtemp_c"
                        :status="day.day.condition.text.split(' ')[0]"
                        ></cardsComp>
                    </div>
                </div>
                <div class="dailyForcast">
                    <div class="top">
                        <h2>good {{ greating() }}</h2>
                        <h2>{{ this.time }}</h2>
                    </div>
                    <mainWedgit
                    :temp="this.current.temp_c" 
                    :hum="this.current.humidity"
                    :wind="this.current.wind_mph"
                    :status="this.condition.text"
                    ></mainWedgit>
                    <h3>Hourly Forcast</h3>
                    <div class="bottom">
                        <cardsComp class="card"
                         v-for="(hour,index) in this.dayForcast" :key="index"
                        :day="hour.time.split(' ')[1]" 
                        :temp="hour.temp_c"
                        :status="hour.condition.text.split(' ')[0]"
                        ></cardsComp>
                    </div>
                </div>
            </div>
            <div class="greating" ref="greating">
                <h1>Welcome To My Weather App</h1>
            </div>
        </div>
</template>

<script>
import mainWedgit from './mainWedgit.vue';
import cardsComp from './cardsComp.vue';
export default {
    name: "fetchApi",
    components: {
        mainWedgit,
        cardsComp,
    },
    data(){
        return {
            apiKey: 'e875e6eb9dbb4cb4bc2183953250204',
            apiCall: "http://api.weatherapi.com/v1/forcast.json?key=$e875e6eb9dbb4cb4bc2183953250204&q=palestine",
            apiForcastCall: "http://api.weatherapi.com/v1/forecast.json?key=e875e6eb9dbb4cb4bc2183953250204&q=London&days=3&aqi=yes&alerts=no",
            value: '',
            date: '',
            time: '',
            hour: '',
            dayName: '',
            current: {},
            condition: {},
            forcast: {},
            location: {},
            dayForcast: {},
            forecastday:[],
        }
    },
    methods: {
        apifetch(e){
            if(e.key == "Enter"){
                this.$refs.main.style.display = 'flex';    
                this.$refs.greating.style.display = 'none';    
                fetch(`https://api.weatherapi.com/v1/forecast.json?key=${this.apiKey}&q=${this.value}&days=7&aqi=yes&alerts=no`)
                .then(response => response.json())
                .then(data => {
                    this.current = data.current;
                    this.condition = data.current.condition;
                    this.forcast = data.forcast;
                    this.forecastday = data.forecast.forecastday;
                    this.location = data.location;
                    const [date, time] = data.location.localtime.split(" ");
                        this.date = date;  // "2025-04-04"
                        this.time = time;  // "03:15"
                        this.hour = time.substring(0,2);
                    this.dayForcast = data.forecast.forecastday[0].hour.slice(0, 6);
                }).catch(err => console.error('error is:',err));
            }
        },
        greating(){
            if(this.hour > 0 && this.hour < 12){
                return 'Morning'
            }else {
                return 'evning'
            }
        },
        getDayName(dateString) {
        return new Date(dateString).toLocaleDateString("en-US", { weekday: 'long' });
        }
    },
    mounted() {
        this.$refs.input.focus(); // Set focus on page load
    }
}
</script>


<style >
* {
    box-sizing: border-box;
}
body {
    background-color: #eee;
}
p {
    padding: 0;
    margin: 0;
}
input {
    padding: 20px;
    border: 0;
    outline: none;
    background-color: #fff;
    font-size: 18px;
    min-width: 250px;
    border-top-left-radius: 20px;
    border-bottom-right-radius: 20px;
    margin: 20px 0;
    box-shadow: 0 0 48px -18px black;
}
.main {
    display: none;
    justify-content: center;
    align-items: center;
    margin: 20px auto;
    width: calc(100vw - 300px);
    background-color: white;
    border-radius: 20px;
    box-shadow: 0 0 48px -18px black;
    color: #6A6A6A;
}
.greating {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 20px auto;
    width: calc(100vw - 300px);
    background-color: white;
    border-radius: 20px;
    box-shadow: 0 0 48px -18px black;
    color: #6A6A6A;
}
@media (max-width: 990px) {
    .main,
    .greating {
        width: calc(100vw - 50px);
    }
}
.weeklyForcast{
    width: 70%;
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
}
.top{
    width: 100%;
    font-size: 18px;
    font-weight: 700;
    font-style: italic;
    margin-bottom: 50px;
}
.weeklyForcast .top {
    display: flex !important;
    justify-content: space-between;
}
.weeklyForcast .top p{
    margin-bottom: 20px;
}
.dailyForcast{
    width: 30%;
    padding: 20px;
    background-color: #eeeeee80;
}
.dailyForcast .center .details .left {
    padding: 0;
    margin: 0 5px;
}
.dailyForcast .center .details .right {
    padding: 0;
    margin: 0 5px;
}
.dailyForcast .center .details .left .degree p {
    font-size: 50px;
    font-weight: normal;
    font-style: italic;
}
.dailyForcast .center .details .left .degree span{
    font-size: 30px;
    font-weight: normal;
    font-style: italic;
}
.dailyForcast .center .details .left p{
    font-size: 16px;
}
.dailyForcast .center .details .right > div i{
    font-size: 15px;
}
.dailyForcast .center .details .right > div p {
    font-size: 14px;
}
.dailyForcast .top h2{
    margin: 0;
    margin-bottom: 20px;
}
.bottom {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(90px,1fr));
    justify-content: center;
    align-items: center;
    margin: 20px auto;
    width: 100%;
}
.bottom .card {
    transition: .3s;
}
.bottom .card:hover ~ .card,
.bottom .card:not(:hover):has(+ .card:hover),
.bottom:hover .card:not(:hover) {
    filter: blur(5px);
    transform: scale(0.9);
}
.bottom .card:hover {
    filter: blur(0);
    transform: scale(1.1);
    box-shadow: 0 0 48px -18px black;
}
@media (max-width: 990px){
    .main {
        flex-direction: column;
    }
    .weeklyForcast,
    .dailyForcast{
        width: 100%;
    }
}
</style>