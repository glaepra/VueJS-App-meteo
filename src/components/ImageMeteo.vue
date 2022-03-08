<template>
  <div class="ParentInformation">
    <div class="BackImg"></div>
    <img :src="require('../assets/IconeMeteo/'+image)" alt="" class="Icone" />
    <h2>{{temp}}</h2>
    <span class="Jour">Lundi</span>

    <div class="flex">
      <div>
        <span>Vent</span>
        <span class="info" id="vent">{{vent}}</span>
      </div>
      <div>
        <span>Humidité</span>
        <span class="info" id="humidite">{{Humidite}}</span>
      </div>
      <div>
        <span>Uv</span>
        <span class="info" id="uv">{{uv}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  Name: "IconeMeteo",
  setup() {},
  mounted() {
    fetch(
      "https://api.weatherbit.io/v2.0/current?city=Mulhouse&country=France&key=220098a3c9b4479cbc065ae1237130c7&lang=fr",
      {
        method: "GET",
      }
    )
      .then((data) => {
        return data.json();
      })
      .then((json) => {
        let reponse = json.data[0];
        
        this.GetImage(reponse["weather"].code);
        this.temp = reponse["temp"] + " °";
        this.uv = Math.round(reponse["uv"]);
        this.vent = Math.round(reponse["wind_spd"]) + " Km/H";
        this.Humidite = Math.round(reponse["rh"]) + " %";

        console.log(reponse);
      })
      .catch((err) => {
        console.error(err);
      });
  },
  methods: {
      GetImage(code) {
          switch (code) {
              case 800:
this.imageTree = "soleil.svg";
                case 802:
                  this.image = "soleilNuage.svg";
                break;
              case 804:
                  this.image = "Nuage.svg";
                  break;
          
              default:
                  break;
          }
      }
  },
  data() {
    return {
      temp: 10,
      uv:0,
      vent:0,
      Humidite:0,
      image : 'Nuage.svg',
    };
  },
};
</script>

<style>
.Icone {
  width: 30%;
  filter: drop-shadow(0px 0px 20px rgba(0, 0, 0, 0.1));
}
.ParentInformation {
  position: relative;
  margin-top: 30px;
}
.BackImg {
  z-index: -1;
  position: absolute;
  top: 50px;
  background: rgb(163, 213, 255);
  width: 100%;
  height: 100%;
  border-radius: 40% 40% 0px 0px;
}
h2 {
  font-size: 50px;
  font-weight: 900;
  color: #fff;
}
.Jour {
  font-size: 18px;
  font-weight: 300;
  color: #fff;
}
.flex {
  display: flex;
  justify-content: space-between;
  margin-top: 30px;
}
.flex > div {
  width: 30%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  color: white;
  font-size: 14px;
}
.info {
  font-size: 18px;
  font-weight: 700;
}
</style>
