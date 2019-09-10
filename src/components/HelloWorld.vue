<template>
    <b-container 
      class="bv-example-row bv-example-row-flex-cols background" 
      v-bind:class="[weather+'Secondary']">
      <div 
        class="backgroundImages"
        v-bind:class="[weather+'Primary']"
      >
        <div class="currentDate">
          <p>{{ someDate | moment("dddd") }}</p>
          <p>{{ someDate | moment("MMMM Do YYYY") }}</p>
        </div>
        <h4 class="overcast">{{overcast}}</h4>
        <div class="detail">
          <p class="temperature">{{(currentTemp).toFixed()}}<span class="dot">°</span><span class="celcius">C</span></p>
          <h6 class="location">{{city}}, {{country}}</h6>
        </div>
      </div>
    </b-container>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return{
      currentTemp: '',
      minTemp: '',
      maxTemp:'',
      sunrise: '',
      sunset: '',
      pressure: '',
      humidity: '',
      wind: '',
      overcast: '', 
      icon: '',
      weather: '',
      city: '',
      country: '',
    }
  },
  mounted: function() {
    this.getDataWeather();
    this.someDate = this.$moment()
  },
  methods: {
    getDataWeather: function() {
			this.$http.get('http://api.openweathermap.org/data/2.5/weather?q=Bandung&units=metric&appid=4ce0ef59925057cc5a52ebff5b654bcb')
			.then(response => {
				this.currentTemp = response.data.main.temp;
        this.minTemp = response.data.main.temp_min;
        this.maxTemp = response.data.main.temp_max;
        this.pressure = response.data.main.pressure;
        this.city = response.data.name;
        this.country = response.data.sys.country;
        this.humidity = response.data.main.humidity + '%';
        this.wind = response.data.wind.speed + 'm/s';
        this.weather = response.data.weather[0].main;
        this.overcast = response.data.weather[0].description;
        this.icon = "images/" + response.data.weather[0].icon.slice(0, 2) + ".svg";
        this.sunrise = new Date(response.data.sys.sunrise*1000).toLocaleTimeString("en-GB").slice(0,4);
        this.sunset = new Date(response.data.sys.sunset*1000).toLocaleTimeString("en-GB").slice(0,4);
			}, err => {
				this.showMessageError(err)
			});
		}
  }
}
</script>