<template>
  <div id="app">
    <h2>Cuenta Regresiva</h2>
    <div class="container">
      <div class="row">
        <div class="col-12">
          <div class="cuadro-fechas">{{ tiempo }} min/seg</div>
            <button v-for="btn in data" :key="btn.time" @click="clic(btn.value)" class="m-4 btn btn-info">
              {{ btn.time }}
            </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

export default {
  name: "App",
  data(){
    return {
      tiempo: 0,
      parar: 0,
      intervalo: "",
      data: [
      {
        time: "3s",
        value: 3
      },
      {
        time: "1m",
        value: 60
      },
      {
        time: "5m",
        value: 300
      },
      {
        time: "10m",
        value: 600
      },
      {
        time: "30m",
        value: 1800
      }
    ]
    }
  },
  methods: {
    clic(value) {
      clearInterval(this.intervalo);
      this.intervalo = setInterval(() =>{
        this.parar =  value--;
        this.tiempo = this.secondsToString(this.parar);
        if (this.parar === 0) {
          clearInterval(this.intervalo);
          return;
        }
      }, 1000);
    },
    secondsToString(seconds) {
      let minute = Math.floor((seconds / 60) % 60);
      minute = (minute < 10)? '0' + minute : minute;
      let second = seconds % 60;
      second = (second < 10)? '0' + second : second;
      return  minute + ':' + second;
    },
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 160px;
}
h2{
  margin: 30px 0 30px;
  font-weight: bold;
}
.btn-info{
  width: 80px;
  color: #fff;
  font-weight: bold;
}
.cuadro-fechas {
  font-size: 30px;
  font-weight: bold;
  color: #9b9b9b;
  border: 1px solid #e1e1e1;
  width: 400px;
  margin: 0 auto;
  border-radius: 10px;
}
@media (max-width: 600px) {
  .cuadro-fechas{
    width: auto;
  }
}

</style>
