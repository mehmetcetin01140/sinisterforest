<template>
  <div>
    <img src="endgame.gif" alt="" v-if="endgame" class="endgame" />
    <div class="charachterselect d-flex " v-if="charachterselection">
      <img src="luna.gif" alt="" class="backgroundstart" />
      <img src="choose.gif" class="chooseyourfighter" />
      <button
        class="choosebutton btn border border-5 border-dark rounded-3 d-flex "
        @click="charachterselected()"
      >
        <strong class="border border-2 border-secondary"> Wolfman</strong>
      </button>
      <button
        class="choosebuttontwo btn border border-5 border-dark rounded-3 d-flex text-dark "
        @click="charachterselectedtwo()"
      >
        <strong class="border border-2 border-secondary">Gwydion</strong>
      </button>
    </div>

    <div class="card bgcolor float-start" style="width: 18rem;">
      <img src="wolfman.jpg" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5>Wolfman</h5>
        <p class="card-text">
          Attack Power: 100
        </p>
        <button
          class="btn btncolor btnone text-danger"
          @click="playeroneskillone()"
          :style="{ opacity: myopacityone }"
          id="skillone"
        ></button>
        <button
          class="btn btncolor btntwo text-danger"
          @click="playeroneskilltwo()"
          :style="{ opacity: myopacitytwo }"
          id="skilltwo"
        ></button>
        <button
          class="btn btncolor btnthree text-danger"
          @click="playeroneskillthree()"
          :style="{ opacity: myopacitythree }"
          id="skillthree"
        ></button>
        <button
          class="btn btncolor btnfour text-danger"
          @click="playeroneskillfour()"
          :style="{ opacity: myopacityfour }"
          id="skillfour"
        ></button>

        <p
          :style="{ width: healthone + '%' }"
          class="healthbarone rounded-3 mt-1"
        ></p>
      </div>
      <h5 class="d-flex justify-content-center">Special Attack :</h5>
      <input
        type="text"
        v-model="specialattackone"
        v-on:keyup.enter="wolfspecial"
        id="specialattackone"
        class=""
      />

      <p>
        <a
          class="btn btn-dark button5 btn-sm mt-1"
          data-bs-toggle="collapse"
          href="#collapseExample"
          role="button"
          aria-expanded="false"
          aria-controls="collapseExample"
        >
          info
        </a>
      </p>
      <div class="collapse " id="collapseExample">
        <div class="card card-body bg-dark text-white">
          If you want to use special attack,write "AAAuuuuu" and press ENTER.It
          Can only be used once.
        </div>
      </div>
    </div>

    <!-- this part for player two -->
    <div class="card bgcolor float-end" style="width: 18rem;">
      <img src="sorcerer.jpg" class="card-img-top resizeimg" alt="..." />
      <div class="card-body">
        <h5>Gwydion</h5>
        <p class="card-text">
          Attack Power: 100
        </p>
        <button
          class="btn btncolor btnfirst text-danger"
          @click="playertwoskillone()"
          :style="{ opacity: myopacityfive }"
          id="skillfive"
        ></button>
        <button
          class="btn btncolor btnsecond text-danger"
          @click="playertwoskilltwo()"
          :style="{ opacity: myopacitysix }"
          id="skillsix"
        ></button>
        <button
          class="btn btncolor btnthird text-danger"
          @click="playertwoskillthree()"
          :style="{ opacity: myopacityseven }"
          id="skillseven"
        ></button>
        <button
          class="btn btncolor btnforth text-danger"
          @click="playertwoskillfour()"
          :style="{ opacity: myopacityeight }"
          id="skilleight"
        ></button>

        <p
          :style="{ width: healthtwo + '%' }"
          class="healthbarone rounded-3 mt-1"
        ></p>
      </div>
      <h5 class="d-flex justify-content-center">Special Attack :</h5>
      <input
        type="text"
        v-model="specialattacktwo"
        v-on:keyup.enter="secondspecial"
        id="specialattacktwo"
      />
      <p>
        <a
          class="btn btn-dark button5 btn-sm mt-1"
          data-bs-toggle="collapse"
          href="#collapseExample"
          role="button"
          aria-expanded="false"
          aria-controls="collapseExample"
        >
          info
        </a>
      </p>
      <div class="collapse " id="collapseExample">
        <div class="card card-body bg-dark text-white">
          If you want to use special attack,write "maledictus es!" and press
          ENTER.It Can only be used once.
        </div>
      </div>
    </div>
    <div class="d-flex justify-content-center ">
      <textarea
        class="d-flex justify-content-center centerarea border border-dark rounded-3 gamelog acax"
        readonly
        v-model="gamelog"
        id="myDIV"
      ></textarea>
    </div>
    <div class="d-flex justify-content-center endgame" v-if="endgame">
      <h5 class="text-white me-3">{{ whowin }}</h5>
      <button class="playagainbutton btn btn-danger" @click="playagain()">
        Play Again
      </button>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main";
import CompTwo from "./CompTwo.vue";
export default {
  data: function() {
    return {
      charachterselection: true,
      botintervaltwo: "",
      botinterval: "",
      healthinterval: "",
      botintervalbloodywolf: "",
      botinervalforhealth: "",
      healthone: 100,
      healthtwo: 100,
      myopacityone: 1,
      myopacitytwo: 1,
      myopacitythree: 1,
      myopacityfour: 1,
      myopacityfive: 1,
      myopacitysix: 1,
      myopacityseven: 1,
      myopacityeight: 1,
      skillonecooldown: "",
      skillfivecooldown: "",
      skillsixcooldown: "",
      skillsevencooldown: "",
      skilleightcooldown: "",
      skilltwointerval: "",
      skillthreeinterval: "",
      skillfourinterval: "",
      skillfiveinterval: "",
      mytime: 0,
      mytimethree: 0,
      mytimefour: 0,
      mytimefive: 0,
      mytimesix: 0,
      mytimeseven: 0,
      mytimeeight: 0,
      cooldownone: "",
      specialattackone: "",
      specialattacktwo: "",
      gamelog: "The fight has begun!",
      infotoggle: false,
      endgame: false,
      whowin: ""
    };
  },
  methods: {
    charachterselected() {
      this.charachterselection = false;
      document.getElementById("skillfive").disabled = true;
      document.getElementById("skillsix").disabled = true;
      document.getElementById("skillseven").disabled = true;
      document.getElementById("skilleight").disabled = true;
      document.getElementById("specialattacktwo").disabled = true;
      return this.botcharachtertwo();
    },
    charachterselectedtwo() {
      this.charachterselection = false;
      document.getElementById("skillone").disabled = true;
      document.getElementById("skilltwo").disabled = true;
      document.getElementById("skillthree").disabled = true;
      document.getElementById("skillfour").disabled = true;
      document.getElementById("specialattackone").disabled = true;
      return this.botcharachterone();
    },
    botcharachterone() {
      this.botintervaltwo = setInterval(
        function() {
          if (this.myopacityone === 1) {
            this.healthtwo -= 13;
          }
        }.bind(this),
        5000
      );
      this.botintervalhorde = setInterval(
        function() {
          if (this.myopacitytwo === 1) {
            this.healthtwo -= 1.5;
          }
        }.bind(this),
        1500
      );
      this.botintervalbloodywolf = setInterval(
        function() {
          if (this.myopacitythree === 1) {
            this.healthtwo -= 15;
          }
        }.bind(this),
        10000
      );
      this.botinervalforhealth = setInterval(
        function() {
          if (this.myopacityfour === 1 && this.healthone < 100) {
            this.healthone += 10;
          }
        }.bind(this),
        15000
      );
    },
    botcharachtertwo() {
      let buttonhunter = Math.floor(Math.random() * 2);

      if (buttonhunter === 0) {
        document.getElementById("skilltwo").disabled = true;
        this.myopacitytwo -= 0.6;
      }
      if (buttonhunter === 1) {
        document.getElementById("skillthree").disabled = true;
        this.myopacitythree -= 0.6;
      }
      if (buttonhunter === 2) {
        document.getElementById("skillfour").disabled = true;
        this.myopacityfour -= 0.6;
      }
      if (this.healthone < 20) {
        this.healthone = 0;
      }
      this.healthinterval = setInterval(
        function() {
          if (this.healthtwo < 100) {
            this.healthtwo += 10;
          }
        }.bind(this),
        15000
      );

      this.botinterval = setInterval(
        function() {
          this.healthone -= 12;
        }.bind(this),
        5000
      );
    },
    playeroneskillone() {
      document.getElementById("myDIV").style.backgroundImage = "url('s1.gif')";
      this.healthtwo -= 7;
      document.getElementById("skillone").disabled = true;
      this.myopacityone -= 0.6;

      this.skillonecooldown = setInterval(
        function() {
          this.cooldownone++;

          if (
            this.cooldownone === 5 ||
            this.cooldownone === 10 ||
            this.cooldownone === 15 ||
            this.cooldownone === 20 ||
            this.cooldownone === 25 ||
            this.cooldownone === 30 ||
            this.cooldownone === 35 ||
            this.cooldownone === 40 ||
            this.cooldownone === 45 ||
            this.cooldownone === 50 ||
            this.cooldownone === 55 ||
            this.cooldownone === 60 ||
            this.cooldownone === 65
          ) {
            document.getElementById("skillone").disabled = false;
            this.myopacityone = 1;
            clearInterval(this.skillonecooldown);
          }
          if (this.healthone <= 0) {
            this.endgame = true;
            this.whowin = "Gwaydion Wins";
          }
          if (this.healthtwo <= 0) {
            this.endgame = true;
            this.whowin = "Wolfman Wins";
          }
        }.bind(this),
        1000
      );
    },
    playeroneskilltwo() {
      document.getElementById("myDIV").style.backgroundImage = "url('s2.gif')";
      document.getElementById("skilltwo").disabled = true;
      this.myopacitytwo -= 0.6;
      this.skilltwointerval = setInterval(
        function() {
          this.healthtwo -= 0.7;
          this.mytime++;
          if (this.mytime === 50) {
            clearInterval(this.skilltwointerval);
          }
        }.bind(this),
        1500
      );
    },
    playeroneskillthree() {
      document.getElementById("myDIV").style.backgroundImage = "url('s3.gif')";
      this.healthtwo -= 15;
      document.getElementById("skillthree").disabled = true;
      this.myopacitythree -= 0.6;
      this.skillthreeinterval = setInterval(
        function() {
          this.mytimethree++;
          if (
            this.mytimethree === 8 ||
            this.mytimethree === 16 ||
            this.mytimethree === 24 ||
            this.mytimethree === 32 ||
            this.mytimethree === 40 ||
            this.mytimethree === 48 ||
            this.mytimethree === 56 ||
            this.mytimethree === 64 ||
            this.mytimethree === 72
          ) {
            document.getElementById("skillthree").disabled = false;
            this.myopacitythree = 1;
            clearInterval(this.skillthreeinterval);
          }
        }.bind(this),
        1500
      );
    },
    playeroneskillfour() {
      document.getElementById("myDIV").style.backgroundImage = "url('s4.gif')";
      this.healthtwo -= 10;
      if (this.healthone < 100) {
        this.healthone += 10;
      }
      document.getElementById("skillfour").disabled = true;
      this.myopacityfour -= 0.6;
      this.skillfourinterval = setInterval(
        function() {
          this.mytimefour++;
          if (
            this.mytimefour === 15 ||
            this.mytimefour === 30 ||
            this.mytimefour === 45 ||
            this.mytimefour === 60 ||
            this.mytimefour === 75
          ) {
            document.getElementById("skillfour").disabled = false;
            this.myopacityfour = 1;
            clearInterval(this.skillfourinterval);
          }
        }.bind(this),
        1500
      );
    },
    playertwoskillone() {
      document.getElementById("myDIV").style.backgroundImage = "url('s5.gif')";
      this.healthone -= 10;
      document.getElementById("skillfive").disabled = true;
      this.myopacityfive -= 0.6;

      this.skillfivecooldown = setInterval(
        function() {
          this.mytimefive++;

          if (
            this.mytimefive === 3 ||
            this.mytimefive === 6 ||
            this.mytimefive === 9 ||
            this.mytimefive === 12 ||
            this.mytimefive === 15 ||
            this.mytimefive === 18 ||
            this.mytimefive === 21 ||
            this.mytimefive === 24 ||
            this.mytimefive === 27 ||
            this.mytimefive === 30 ||
            this.mytimefive === 33 ||
            this.mytimefive === 36 ||
            this.mytimefive === 39 ||
            this.mytimefive === 42 ||
            this.mytimefive === 45 ||
            this.mytimefive === 48 ||
            this.mytimefive === 51 ||
            this.mytimefive === 54 ||
            this.mytimefive === 57 ||
            this.mytimefive === 60 ||
            this.mytimefive === 63 ||
            this.mytimefive === 66 ||
            this.mytimefive === 69 ||
            this.mytimefive === 72 ||
            this.mytimefive === 75 ||
            this.mytimefive === 78 ||
            this.mytimefive === 81 ||
            this.mytimefive === 84 ||
            this.mytimefive === 87 ||
            this.mytimefive === 90 ||
            this.mytimefive === 93 ||
            this.mytimefive === 96 ||
            this.mytimefive === 99
          ) {
            document.getElementById("skillfive").disabled = false;
            this.myopacityfive = 1;
            clearInterval(this.skillfivecooldown);
          }
          if (this.healthone <= 0) {
            this.endgame = true;
            this.whowin = "Gwydion Wins";
          }
          if (this.healthtwo <= 0) {
            this.endgame = true;
            this.whowin = "Wolfman Wins";
          }
        }.bind(this),
        1000
      );
    },
    playertwoskilltwo() {
      document.getElementById("myDIV").style.backgroundImage = "url('s6.gif')";
      if (this.healthtwo < 100) {
        this.healthtwo += 15;
      }
      document.getElementById("skillsix").disabled = true;
      this.myopacitysix -= 0.6;

      this.skillsixcooldown = setInterval(
        function() {
          this.mytimesix++;

          if (
            this.mytimesix === 0 ||
            this.mytimesix === 15 ||
            this.mytimesix === 30 ||
            this.mytimesix === 45 ||
            this.mytimesix === 60 ||
            this.mytimesix === 75 ||
            this.mytimesix === 90 ||
            this.mytimesix === 105 ||
            this.mytimesix === 120 ||
            this.mytimesix === 135 ||
            this.mytimesix === 150 ||
            this.mytimesix === 165 ||
            this.mytimesix === 180
          ) {
            document.getElementById("skillsix").disabled = false;
            this.myopacitysix = 1;
            clearInterval(this.skillsixcooldown);
          }
        }.bind(this),
        1000
      );
    },
    playertwoskillthree() {
      document.getElementById("myDIV").style.backgroundImage = "url('s7.gif')";
      let buttonhunter = Math.floor(Math.random() * 2);

      if (buttonhunter === 0) {
        document.getElementById("skilltwo").disabled = true;
        this.myopacitytwo -= 0.6;
      }
      if (buttonhunter === 1) {
        document.getElementById("skillthree").disabled = true;
        this.myopacitythree -= 0.6;
      }
      if (buttonhunter === 2) {
        document.getElementById("skillfour").disabled = true;
        this.myopacityfour -= 0.6;
      }

      document.getElementById("skillseven").disabled = true;

      this.myopacityseven -= 0.6;

      this.skillsevencooldown = setInterval(
        function() {
          this.mytimeseven++;

          if (this.mytimeseven === 400) {
            document.getElementById("skillseven").disabled = false;
            this.myopacityseven = 1;
            clearInterval(this.skillsevencooldown);
          }
        }.bind(this),
        1000
      );
    },
    playertwoskillfour() {
      if (this.healthone < 20) {
        this.healthone = 0;
      }
      document.getElementById("myDIV").style.backgroundImage = "url('s8.gif')";
      document.getElementById("skilleight").disabled = true;
      this.myopacityeight -= 0.6;

      this.skilleightcooldown = setInterval(
        function() {
          this.mytimeeight++;

          if (this.mytimeeight === 30) {
            document.getElementById("skilleight").disabled = false;
            this.myopacityeight = 1;
            clearInterval(this.skilleightcooldown);
          }
        }.bind(this),
        1000
      );
    },
    wolfspecial: function() {
      if (this.specialattackone === "AAAuuuuu") {
        this.healthtwo -= 20;
        document.getElementById("specialattackone").disabled = true;
      }
    },
    secondspecial: function() {
      if (this.specialattacktwo === "maledictus es!") {
        this.healthone -= 20;
        document.getElementById("specialattacktwo").disabled = true;
      }
    },
    playagain() {
      location.reload();
    }
  },

  components: {
    CompTwo
  }
};
</script>
<style scoped>
.bgcolor {
  background-color: rgba(137, 144, 185, 0.863);
}
.btncolor {
  background-color: rgb(39, 22, 19);
  width: 60px;
  height: 60px;
}
.btnone {
  background-image: url("skilltwo.jpg");
  background-size: cover;
}
.btntwo {
  background-image: url("skillthree.jpg");
  background-size: cover;
}
.btnthree {
  background-image: url("skillfour.jpg");
  background-size: cover;
}
.btnfour {
  background-image: url("skillone.jpg");
  background-size: cover;
}
.btnfirst {
  background-image: url("magic1.jpg");
  background-size: cover;
}
.btnsecond {
  background-image: url("magic2.jpg");
  background-size: cover;
}
.btnthird {
  background-image: url("magic3.jpg");
  background-size: cover;
}
.btnforth {
  background-image: url("magic4.jpg");
  background-size: cover;
}
.healthbarone {
  width: 100%;
  height: 25px;
  background-color: rgb(121, 2, 2);
  transition: width 500ms;
  margin: auto;
}
.resizeimg {
  height: 393.1px;
}
.centerarea {
  width: 50%;
  height: 500px;
  margin-top: 85px;
  background-color: rgba(15, 15, 15, 0.616);
  color: white;
  white-space: pre;
  resize: none;
}

.backgroundstart {
  width: 100%;
  max-width: 100%;
  max-height: 100%;
  position: absolute;
  z-index: 1;
}
.chooseyourfighter {
  z-index: 1;
  width: 400px;
  position: absolute;
  margin-top: 150px;
  margin-left: 790px;
}
.choosebutton {
  position: absolute;
  z-index: 2;
  background-image: url("wolfman.jpg");
  background-size: cover;
  width: 200px;
  height: 400px;
  margin-top: 200px;
  margin-left: 760px;
}
.choosebuttontwo {
  position: absolute;
  z-index: 2;
  background-image: url("sorcerer.jpg");
  background-size: cover;
  width: 200px;
  height: 400px;
  margin-top: 200px;
  margin-left: 1000px;
}
strong {
  background-color: rgba(196, 189, 189, 0.74);
  align-items: center;
  border-radius: 3px;
  margin-top: 340px;
  margin-left: 50px;
}
.gamelog {
  overflow: hidden;
  white-space: pre-line;
}
.button5 {
  border-radius: 50%;
  height: auto;
  width: 100px;
}
.acax {
  background-image: url("");
  width: 800px;
  height: 500px;
  background-size: cover;
}
.endgame {
  background-size: cover;
  position: absolute;
  width: 100%;
  max-width: 100%;
  max-height: 100%;
  z-index: 3;
}
</style>
