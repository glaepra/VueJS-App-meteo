<template>
  <div class="ParentInformationAutreJours">
    <div class="flex">
      <div>
        <span>{{ oneDay }}</span>
        <img
          :src="require('../assets/IconeMeteo/' + imageOne)"
          alt=""
          class="Icone"
        />
        <span class="info">{{ tmpOne }}</span>
      </div>
      <div>
        <span>{{ twoDay }}</span>
        <img
          :src="require('../assets/IconeMeteo/' + imageTwo)"
          alt=""
          class="Icone"
        />
        <span class="info">{{ tmpTwo }}</span>
      </div>
      <div>
        <span>{{ treeDay }}</span>
        <img
          :src="require('../assets/IconeMeteo/' + imageTree)"
          alt=""
          class="Icone"
        />
        <span class="info">{{ tmpTree }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  Name: "autreJours",
  setup() {},
  mounted() {
    fetch(
      "https://api.weatherbit.io/v2.0/forecast/daily?city=Mulhouse&country=France&lang=fr&key=220098a3c9b4479cbc065ae1237130c7",
      {
        method: "GET",
        "content-type": "application/json; charset=utf-8",
        "keep-alive": "timeout=5",
      }
    )
      .then((data) => {
        return data.json();
      })
      .then((json) => {
        console.log(json);
        let reponse = json.data[1];

        this.getImageOne(reponse["weather"].code);
        this.tmpOne = reponse["temp"] + " °";
        this.oneDay = new Date(reponse["datetime"]).toDateString('fr');

        reponse = json.data[2];

        this.getImageTow(reponse["weather"].code);
        this.tmpTwo = reponse["temp"] + " °";
        this.twoDay = new Date(reponse["datetime"]).toDateString('fr');

        reponse = json.data[3];

        this.getImageTree(reponse["weather"].code);
        this.tmpTree = reponse["temp"] + " °";
        this.treeDay = new Date(reponse["datetime"]).toDateString('fr');
      })
      .catch((err) => {
        console.error(err);
      });
  },
  methods: {
    getImageOne(code) {
      switch (code) {
        case 800:
          this.imageOne = "soleil.svg";
          break;
        case 802:
          this.imageOne = "soleilNuage.svg";
          break;
        case 804:
          this.imageOne = "Nuage.svg";
          break;

        default:
          break;
      }
    },
    getImageTow(code) {
      switch (code) {
        case 800:
          this.imageTwo = "soleil.svg";
        case 802:
          this.imageTwo = "soleilNuage.svg";
          break;
        case 804:
          this.imageTwo = "Nuage.svg";
          break;

        default:
          break;
      }
    },
    getImageTree(code) {
      switch (code) {
        case 800:
          this.imageTree = "soleil.svg";
        case 802:
          this.imageTree = "soleilNuage.svg";
          break;
        case 804:
          this.imageTree = "Nuage.svg";
          break;

        default:
          break;
      }
    },
  },
  data() {
    return {
      oneDay: 0,
      twoDay: 0,
      treeDay: 0,
      tmpOne: 0,
      tmpTwo: 0,
      tmpTree: 0,

      imageOne: "Nuage.svg",
      imageTwo: "Nuage.svg",
      imageTree: "Nuage.svg",
    };
  },
};
</script>
<style>
.Icone {
  width: 30%;
  filter: drop-shadow(0px 0px 20px rgba(0, 0, 0, 0.1));
}
.ParentInformationAutreJours {
  position: relative;
  border-top: 1px solid #ffffff24;
  margin-top: 30px;
  padding-bottom: 30px;
  background: #a2d5ff;
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
