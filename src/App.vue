<template>
  <v-app>
    <p justify="start" align="start">Number of bubbles = {{ this.nbBubbles }}</p>
    <p justify="start" align="start">Number of farm 1 = {{ this.nbFarm_1 }}</p>
    <p justify="start" align="start">Number of farm 2= {{ this.nbFarm_2 }}</p>
    <p justify="start" align="start">Number of farm 3= {{ this.nbFarm_3 }}</p>
    <v-row justify="center">
      <v-btn color="green" @click="addFarm_1">Buy farmlevel_1</v-btn>
      <v-spacer></v-spacer>
      <v-btn color="green" @click="addFarm_2">Buy farmlevel_2</v-btn>
      <v-spacer></v-spacer>
      <v-btn color="green" @click="addFarm_3">Buy farmlevel_3</v-btn>
    </v-row>
    <v-row justify="start" align="center">
        <img :src="bub_1" @click="add_bubble_game" height="100px" width="100px">
        <v-spacer></v-spacer>
        <img :src="bos_1" @click="removeBubble" height="200px" width="150px">
    </v-row>
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
    setInterval(() => {
      this.nbBubbles += this.nbFarm_1;
      if (this.nbFarm_2 != 0)
        this.nbBubbles += this.nbFarm_2 + 2;
      if (this.nbFarm_3 != 0)
        this.nbBubbles += this.nbFarm_3 + 3;
      this.$forceUpdate();
    }, 1000)
  },
  created () {
    this.nbBubbles = 0,
    this.nbFarm_1= 0,
    this.nbFarm_2 = 0,
    this.nbFarm_3 = 0
  },
  methods: {
    add_bubble_game () {
      this.nbBubbles += 1;
      console.log(this.nbBubbles);
      this.$forceUpdate();
    },
    removeBubble () {
      if (this.nbBubbles <= 0)
        return;
      this.nbBubbles -= 1;
      console.log(this.nbBubbles);
      this.$forceUpdate();
    },
    addFarm_1 () {
      if (this.nbBubbles < (this.nbFarm_1 + 30))
        return;
      this.nbBubbles -= (this.nbFarm_1 + 30);
      this.nbFarm_1 += 1;
      this.$forceUpdate();
    },
    addFarm_2 () {
      if (this.nbBubbles < (this.nbFarm_2 + 60))
        return;
      this.nbBubbles -= (this.nbFarm_2 + 60);
      this.nbFarm_2 += 1;
      this.$forceUpdate();
    },
    addFarm_3 () {
      if (this.nbBubbles < (this.nbFarm_3 + 100))
        return;
      this.nbBubbles -= (this.nbFarm_3 + 100);
      this.nbFarm_3 += 1;
      this.$forceUpdate();
    }
  }
};
</script>
