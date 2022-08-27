<template>
  <div
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.list[0].main.temp > 16
        ? 'warm'
        : ''
    "
  >
    <header><Navbar /></header>
    <main>
      <div class="dropdown-popover" @click="isVisible = !isVisible">
        <div class="search-box">
          <input
            type="text"
            class="search-bar"
            placeholder="Search..."
            v-model="query"
            @keypress="fetchWeather"
            @keyup="searchTimeOut()"
          />
        </div>
        <div class="options" v-if="isVisible">
          <ul class="ul">
            <li
              @click="selectItem(weather)"
              v-for="weather in filteredWeather"
              :key="weather.title"
            >
              {{ weather.name.common }}
            </li>
          </ul>
        </div>
      </div>

      <div class="weather-wrap" v-if="typeof weather.cod != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.city.name }}, {{ weather.city.country }}
          </div>
          <div class="date">{{ weather.list[0].dt_txt }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.list[0].main.temp) }}°c</div>
          <div class="weather">{{ weather.list[0].weather[0].main }}</div>
        </div>
      </div>

      <div class="container">
        <div class="grid">
          <article>
            <div class="weather-wrap" v-if="typeof weather.cod != 'undefined'">
              <div class="location-box">
                <div class="location">
                  {{ dateBuilder(1) }}
                </div>
                <div class="date">{{ weather.list[5].dt_txt }}</div>
              </div>

              <div class="weather-box">
                <div class="temp">
                  {{ Math.round(weather.list[5].main.temp) }}°c
                </div>
                <div class="weather">{{ weather.list[5].weather[0].main }}</div>
              </div>
            </div>
          </article>
          <article>
            <div class="weather-wrap" v-if="typeof weather.cod != 'undefined'">
              <div class="location-box">
                <div class="location">
                  {{ dateBuilder(2) }}
                </div>
                <div class="date">{{ weather.list[13].dt_txt }}</div>
              </div>

              <div class="weather-box">
                <div class="temp">
                  {{ Math.round(weather.list[13].main.temp) }}°c
                </div>
                <div class="weather">
                  {{ weather.list[13].weather[0].main }}
                </div>
              </div>
            </div>
          </article>
          <article>
            <div class="weather-wrap" v-if="typeof weather.cod != 'undefined'">
              <div class="location-box">
                <div class="location">
                  {{ dateBuilder(3) }}
                </div>
                <div class="date">{{ weather.list[21].dt_txt }}</div>
              </div>

              <div class="weather-box">
                <div class="temp">
                  {{ Math.round(weather.list[21].main.temp) }}°c
                </div>
                <div class="weather">
                  {{ weather.list[21].weather[0].main }}
                </div>
              </div>
            </div>
          </article>
          <article>
            <div class="weather-wrap" v-if="typeof weather.cod != 'undefined'">
              <div class="location-box">
                <div class="location">
                  {{ dateBuilder(4) }}
                </div>
                <div class="date">{{ weather.list[29].dt_txt }}</div>
              </div>

              <div class="weather-box">
                <div class="temp">
                  {{ Math.round(weather.list[29].main.temp) }}°c
                </div>
                <div class="weather">
                  {{ weather.list[29].weather[0].main }}
                </div>
              </div>
            </div>
          </article>
          <article>
            <div class="weather-wrap" v-if="typeof weather.cod != 'undefined'">
              <div class="location-box">
                <div class="location">
                  {{ dateBuilder(5) }}
                </div>
                <div class="date">{{ weather.list[37].dt_txt }}</div>
              </div>

              <div class="weather-box">
                <div class="temp">
                  {{ Math.round(weather.list[37].main.temp) }}°c
                </div>
                <div class="weather">
                  {{ weather.list[37].weather[0].main }}
                </div>
              </div>
            </div>
          </article>
          <article>
            <div class="weather-wrap" v-if="typeof weather.cod != 'undefined'">
              <div class="location-box">
                <div class="location">
                  {{ dateBuilder(6) }}
                </div>
                <div class="date">{{ weather.list[38].dt_txt }}</div>
              </div>

              <div class="weather-box">
                <div class="temp">
                  {{ Math.round(weather.list[38].main.temp) }}°c
                </div>
                <div class="weather">
                  {{ weather.list[38].weather[0].main }}
                </div>
              </div>
            </div>
          </article>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  components: { Navbar },
  data() {
    return {
      api_key: "549310631a641754754a1b343fcccd74",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
      weatherArray: [],
      isVisible: false,
      selectedItem: null,
    };
  },
  computed: {
    filteredWeather() {
      const querry = this.query.toLowerCase();
      if (this.query === "") {
        return this.weatherArray;
      }
      return this.weatherArray.filter((weather) => {
        return Object.values(weather).some((word) =>
          String(word).toLowerCase().includes(querry)
        );
      });
    },
  },
  mounted() {
    fetch(`https://restcountries.com/v3.1/all`)
      .then((res) => {
        return res.json();
      })
      .then((json) => {
        this.weatherArray = json;
      });
  },
  methods: {
    searchTimeOut() {
      if (this.timer) {
        clearTimeout(this.timer);
        this.timer = null;
      }
      this.timer = setTimeout(() => {
        fetch(
          `https://api.openweathermap.org/data/2.5/forecast?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }, 1500);
    },
    selectItem(weather) {
      console.log("select item", weather);
      this.query = weather.name.common;

      fetch(
        `https://api.openweathermap.org/data/2.5/forecast?q=${this.query}&units=metric&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `https://api.openweathermap.org/data/2.5/forecast?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder(dt) {
      let d = new Date();

      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let m = d.getDay() + dt;
      if (m > 6) {
        m = d.getDay() - (7 - dt);
      }
      let day = days[m];

      return `${day}`;
    },
  },
};
</script>

<style>
#app {
  background-image: url("./images/cloud.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.warm {
  background-image: url("./images/warm-bg.jpg");
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "montserrat";
}
header {
  width: 100vw;
  background-color: black;
  padding: 15px;
}
main {
  min-height: 100vh;
  padding: 25px;
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.dropdown-wrapper {
  position: relative;
  margin: 0 auto;
}

.options {
  width: 100%;
}
.ul {
  list-style: none;
  text-align: left;
  max-height: 150px;
  padding-left: 8px;
  overflow-y: scroll;
}
li {
  width: 100%;
  border-bottom: 1px solid lightgray;
  padding: 10px;
  cursor: pointer;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-gap: 2rem;
  align-items: flex-start;
  padding: 40px;
  justify-content: space-around;
}
.grid > article {
  border: none;
  border-radius: 20px;
  text-align: center;
  width: 300px;
}
</style>
