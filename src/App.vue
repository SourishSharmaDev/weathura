<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Type The Location...."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-cont" v-if="typeof weather.main != 'undefined'">
        <br />
        <div class="weather-info">
          <div class="weather">{{ weather.weather[0].main }}</div>
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
        </div>
        <div class="location-info">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ getDate() }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {},
  data() {
    return {
      api_key: "abad26a1cd28d3a5fd6d3e43152a0f7f",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(result) {
      this.weather = result;
    },
    getDate() {
      let d = new Date();
      let months = [
        "January",
        "Febuary",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = ["Mon", "Tue", "Wed", "Thurs", "Fri", "Sat", "Sun"];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      let day = days[d.getDay()];

      return `${day} ${date} ${month}, ${year}`;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300&family=Odibee+Sans&family=Poppins:wght@200&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Odibee+Sans&family=Sigmar+One&family=Staatliches&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Noto Sans JP", sans-serif;
  padding: 20px;
  background-image: linear-gradient(#e52165, #0d1137);
  height: 100%;
  margin: 0;
  background-repeat: no-repeat;
  background-attachment: fixed;
  transition: 1s ease-in-out;
}

#app {
  /* background-image: url('./josh-hild-_TuI8tZHlk4-unsplash.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 1s; */
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #fff;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 1px 3px;
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 25px 25px 25px 5px;
  transition: 0.4s ease-in-out;
}

.search-box .search-bar:focus {
  box-shadow: 0px 2px 8px gray;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 5px 5px 5px 5px;
}

.search-box .search-bar::placeholder {
  font-family: "Noto Sans JP", sans-serif;
}

.location-info .location {
  text-align: center;
  font-family: "Poppins", sans-serif;
  color: #fff;
  font-size: 50px;
  font-weight: 1000;
  text-shadow: 1px 3px rgba(255, 255, 255, 0.2);
}

.location-info .date {
  text-align: center;
  font-family: "Poppins", sans-serif;
  color: rgb(156, 123, 218);
  font-style: italic;
  font-size: 30px;
  font-weight: 700;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.2);
}

.weather-info {
  text-align: center;
  font-family: "Poppins", sans-serif;
}

.weather-info .temp {
  font-family: "Odibee Sans", cursive;
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px 6px rgba(255, 255, 255, 0.2);
  background-color: rgba(53, 53, 53, 0.5);
  border-radius: 10px 5px 10px 5px;
  margin: 30px 0px;

  box-shadow: 3px 6px 6px rgba(255, 255, 255, 0.2);
}

.weather-info .weather {
  font-family: 'Staatliches', cursive;
  letter-spacing: 4px;
  font-size: 50px;
  font-weight: 300;
  color: #fff;
  font-style: italic;
  text-shadow: 1px 2px 2px rgba(255, 255, 255, 0.2);
}
</style>
