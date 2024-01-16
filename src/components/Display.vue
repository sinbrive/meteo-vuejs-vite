<template>
  <div id="api">
    <div class="left">
      <div id="ville">{{data.name}}</div>
      <div class="date">
        <div id="jour">{{day}}</div>
        <div id="jour">{{date}}</div>
        <div id="mois">{{month}}</div>
      </div>
      
      <div class="temp">
         <p><i class="fas fa-temperature-high"></i>{{ temp }}°C</p>
         <p><span>ressentie</span> {{ feels_like }}°C</p>
         <p>{{ temp_min }}/{{ temp_max }}°C</p>
      </div>

    </div>
    <div class="middle">
      <div id="icon"><img :src="icon_path" /></div>
      <div id="overall">{{ data.weather[0].description }}</div>
    </div>
    <div class="right">
      <div class="sun">
        <div>
          <span><i class="fas fa-sun"></i></span><span>{{ sunrise }}</span>
        </div>
        <div>
          <span><i class="fas fa-moon"></i></span><span>{{ sunset }}</span>
        </div>
      </div>
      <div>
         <span><i class="fas fa-percent"></i>{{ data.main.humidity }}</span>
      </div>
      <div id="wind">
        <div id="vvent"><i class="fas fa-wind"></i>{{ data.wind.speed }} km/h</div>
        <div id="orientation"><i class="fas fa-location-arrow"></i>{{ data.wind.deg }}°</div>
      </div>
      <div id="pressure"><p><i class="fas fa-compress"></i>{{ data.main.pressure }}mb</p></div>
      </div>
  </div>
</template>

<script>

import {computed} from 'vue'

export default {
  props: 
    ['data', 'icon_path']
  , 
  data() {
    return {
      temp: null,
      temp_max: null,
      temp_min: null,
      feels_like: null,
      day: null,
      month: null,
      date: null,
      week: ['Dim', 'Lun', 'Mar', 'Mer', 'Jeu', 'Vend', 'Sam'],
      year: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec'],
      sunset: null,
      sunrise: null
    };
  },
  mounted() {
    this.getDate();
    this.getDay();
    this.getMonth();
    this.temp=(this.data.main.temp).toFixed(1)
    this.temp_min=(this.data.main.temp_min).toFixed(1)
    this.temp_max=(this.data.main.temp_max).toFixed(1)
    this.feels_like=(this.data.main.feels_like).toFixed(1)
    this.getSunset();
    this.getSunrise();
    
  },
  methods: {
    update()  {
      this.$emit('updateData')
    },
    getSunset(){
      this.sunset = computed(()=> {
          let dt = new Date(this.data.sys.sunset*1000)
          return dt.getHours()+":"+dt.getMinutes()
      })
    }, 
    getSunrise(){
      this.sunrise = computed(()=> {
          let dt = new Date(this.data.sys.sunrise*1000)
          return dt.getHours()+":"+dt.getMinutes()
      })
    },
    getDay(){
      this.day = computed(()=> {
          let dt = new Date(this.data.sys.sunset*1000)
          return this.week[dt.getDay()]
      })
    },
    getMonth(){
      this.month = computed(()=> {
          let dt = new Date(this.data.sys.sunset*1000)
          return this.year[dt.getMonth()]
      })
    },
    getDate(){
      this.date = computed(()=> {
          let dt = new Date(this.data.sys.sunset*1000)
          return dt.getDate()
      })
    },
    
  }
};
</script>

<style>
</style>