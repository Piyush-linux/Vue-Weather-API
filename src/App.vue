<template>
        <div class="container">
            <!-- search -->
            <div class="row" align="center">
                <input 
                type="text" 
                name="city" 
                placeholder="Search..." 
                class="u-full-width"
                @input="city($event)"
                />
                <button type="button" @click="weather">submit</button>
            </div>
            <!-- weather -->
            <div class="row weather" v-if="lock">
              <h1 class="lock"> {{data.temp}} C </h1>
              <h5 class="lock"> {{data.city}} </h5>
              <h4 class="lock"> {{data.cloud}} </h4>
            </div>
         
        </div>
</template>
<script>
export default {
    name: 'App',
    data() {
        return {
          api_key:'fe000ea81fc76b6904399b3f47ddff19',
            loc:'',
            data:{},
            lock:false,
        }
    },
    methods: {
      weather(){
        let data = async ()=> { 
          let url=`http://api.openweathermap.org/data/2.5/weather?q=${this.loc},in&appid=${this.api_key}`
          let raw = await ( await fetch(url)).json() 
          this.data.temp= Math.floor(raw.main.temp-274)
          this.data.city= raw.name
          this.data.cloud= raw.weather[0].main
          this.lock=true
        }
        data()
      },
      city(e){
        this.loc=e.target.value
        console.log(this.loc)
      }
    }
}
</script>
<style> 
body{
  margin: 0;
  padding: 0;
  width: 100vw;
  height:100vh;
}
.container{
    margin-top: 5em;
}
#app {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    /*background-color: #454356*/
}
.row{
  content:none; 
}
.weather{
  margin-top: 3em;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;


}
input{
  padding: .5em;
  font-family: Hermit;
  letter-spacing: 2px;
}
</style>