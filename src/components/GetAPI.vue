<template>
  <div></div>
</template>

<script>

export default {
  components: {
  },
  data() {
    return {
      title: "Get API",
      isloading: true,
      json: null,
      path: "https://openweathermap.org/img/w/",
      url: "https://api.openweathermap.org/data/2.5/weather?lat=48&lon=0.19652&units=metric&appid="+import.meta.env.VITE_APP_APIKEY+"&lang=fr",
    };
  },
  created() {
    fetch(this.url)
    .then((response) => {
      return response.json();
    })
    .then((data) => {
      console.log(this.url)
      this.json = data;
      this.path += `${this.json.weather[0].icon}` + ".png";
      this.isloading=false;
      this.$emit('data_received', {data: this.json,
                       path: this.path})
    });
  },
  methods:{
   
  }
};
</script>

<style>
</style>