<template>
  <v-app :style="{ backgroundColor:'#aa98b8' }">
    <v-card color="red" class="py-5 px-5" elevation="10" outlined>
      <v-row>
        Number of bubbles = {{ this.nbBubbles }}
        <v-spacer></v-spacer>
        damage of boss = {{ this.nbboss }}
        <v-spacer></v-spacer>
        Number of farm 1 = {{ this.nbFarm_1 }}
        <v-spacer></v-spacer>
        Number of farm 2= {{ this.nbFarm_2 }}
        <v-spacer></v-spacer>
        Number of farm 3= {{ this.nbFarm_3 }}
      </v-row>
    </v-card>
    <v-row justify="center">
      <v-col>
        <v-card color="#dcadff" class="py-5 px-5" elevation="0" outlined>
          <v-row>
            <v-col>
              <v-btn class="ma-12" @click="addFarm_1">Buy farmlevel_1</v-btn>
            </v-col>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-col>
              <v-btn class="ma-12" @click="addFarm_2">Buy farmlevel_2</v-btn>
            </v-col>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-col>
              <v-btn class="ma-12" @click="addFarm_3">Buy farmlevel_3</v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
    <v-row align="start">
      <v-col>
        <v-card color="#dcadff" class="px-5" elevation="0" outlined>
          <v-row>
            <v-col>
              <img :src="lev_1" height="200px" width="200px">
            </v-col>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-col>
              <img :src="lev_2" height="200px" width="200px">
            </v-col>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-col>
              <img :src="lev_3" height="200px" width="200px">
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
    <v-row align="start">
      <v-col>
        <v-card color="#dcadff" class="px-5" elevation="0" outlined>
          <v-row>
            <v-col>
              <v-progress-linear height="20px" :value="life_bubble"></v-progress-linear>
              <img :src="bub_1" @click="add_bubble_game" height="300px" width="300px">
            </v-col>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-col>
              <v-progress-linear height="20px" :value="life"></v-progress-linear>
              <img :src="bos_1" @click="removeBubble" height="300px" width="300px">
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog v-model="win" width="200">
      <v-card>
          <h1>BRAVO !</h1>
          <img :src="bub_3" @click="refresh" height="200px" width="200px"/>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="white" @click="refresh">restart</v-btn>
            <v-spacer></v-spacer>
          </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog v-model="lose" width="200">
      <v-card>
          <h1>OH NON !</h1>
          <img :src="bub_3" @click="refresh" height="200px" width="200px"/>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="white" @click="refresh">restart</v-btn>
            <v-spacer></v-spacer>
          </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import bubble_1 from './assets/test.png'
import bubble_2 from './assets/bulle_2.png'
import bubble_3 from './assets/bulle_3.png'
import level_1 from './assets/flacon.png'
import level_2 from './assets/big_bubble.jpg'
import level_3 from './assets/level_3.png'
import bonus_1 from './assets/bonus_1.jpg'
import bonus_2 from './assets/bonus_2.jpg'
import bonus_3 from './assets/bonus_3.png'
import boss_1 from './assets/boss_1.jpg'
import boss_2 from './assets/boss_2.png'
import boss_3 from './assets/boss_3.png'
import not_son from './assets/not_son.png'
import play_son from './assets/play_son.png'
export default {
  name: 'App',

  data: () => ({
    bub_1: bubble_1,
    bub_2: bubble_2,
    bub_3: bubble_3,
    lev_1: level_1,
    lev_2: level_2,
    lev_3: level_3,
    bon_1: bonus_1,
    bon_2: bonus_2,
    bon_3: bonus_3,
    bos_1: boss_1,
    bos_2: boss_2,
    bos_3: boss_3,
    off_son: not_son,
    on_son: play_son
  }),
  mounted () {
    if (this.nbBubbles <= 0)
      this.game_over();
    setInterval(() => {
      this.nbBubbles += this.nbFarm_1;
      if (this.nbFarm_2 != 0)
        this.nbBubbles += this.nbFarm_2 + 2;
      if (this.nbFarm_3 != 0)
        this.nbBubbles += this.nbFarm_3 + 3;
      this.life = ((this.damage / 1000) * 100);
      this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100);
      this.$forceUpdate();
    }, 1000)
    setInterval(() => {
      this.nbBubbles -= this.nbboss;
      this.life = ((this.damage / 1000) * 100);
      this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100);
      this.$forceUpdate();
    }, 10000)
  },
  created () {
    this.nbBubbles = 100,
    this.damage_bubble = 1000,
    this.damage = 1000,
    this.life = ((this.damage / 1000) * 100),
    this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100),
    this.nbFarm_1= 0,
    this.nbFarm_2 = 0,
    this.nbFarm_3 = 0,
    this.nbboss = this.nbFarm_1 + (this.nbFarm_2 + 1) + (this.nbFarm_3 + 2),
    this.win = false,
    this.lose = false
  },
  methods: {
    add_bubble_game () {
      this.nbBubbles += 1;
      this.nbboss = this.nbFarm_1 + (this.nbFarm_2 + 1) + (this.nbFarm_3 + 2);
      this.life = ((this.damage / 1000) * 100);
      this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100);
      console.log(this.nbBubbles);
      this.$forceUpdate();
      this.game_over();
    },
    removeBubble () {
      if (this.nbBubbles <= 0)
        return;
      this.nbBubbles -= 1;
      this.damage -= 1;
      this.life = ((this.damage / 1000) * 100);
      this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100);
      console.log(this.nbBubbles);
      this.$forceUpdate();
      this.game_over();
    },
    addFarm_1 () {
      if (this.nbBubbles < (this.nbFarm_1 + 30))
        return;
      this.nbBubbles -= (this.nbFarm_1 + 30);
      this.nbFarm_1 += 1;
      this.nbboss = this.nbFarm_1 + (this.nbFarm_2 + 1) + (this.nbFarm_3 + 2);
      this.life = ((this.damage / 1000) * 100);
      this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100);
      this.$forceUpdate();
      this.game_over();
    },
    addFarm_2 () {
      if (this.nbBubbles < (this.nbFarm_2 + 60))
        return;
      this.nbBubbles -= (this.nbFarm_2 + 60);
      this.nbFarm_2 += 1;
      this.nbboss = this.nbFarm_1 + (this.nbFarm_2 + 1) + (this.nbFarm_3 + 2);
      this.life = ((this.damage / 1000) * 100);
      this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100);
      this.$forceUpdate();
      this.game_over();
    },
    addFarm_3 () {
      if (this.nbBubbles < (this.nbFarm_3 + 100))
        return;
      this.nbBubbles -= (this.nbFarm_3 + 100);
      this.nbFarm_3 += 1;
      this.nbboss = this.nbFarm_1 + (this.nbFarm_2 + 1) + (this.nbFarm_3 + 2);
      this.life = ((this.damage / 1000) * 100);
      this.life_bubble = ((this.nbBubbles / this.damage_bubble) * 100);
      this.$forceUpdate();
      this.game_over();
    },
    game_over () {
      console.log("life = " + this.life + "life_bubble = " + this.life_bubble);
      if (this.life <= 0) {
        console.log("win");
        this.win = true;
      }
      if (this.life_bubble <= 0.5) {
        console.log("dead");
        this.lose = true;
      }
    },
    refresh () {
      location.reload();
    },
  }
};
</script>
