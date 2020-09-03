<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-6 p-5">
          <app-player :health="playerHealth"></app-player>
        </div>
        <div class="col-md-6 p-5">
          <app-monster :health="monsterHealth"></app-monster>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <app-commands @pReset="playerHealth = $event" @mReset="monsterHealth = $event" :pHealth="playerHealth" :mHealth="monsterHealth"  @playerAttack="pAttack($event)" @playerHeal="playerHealth += $event" @playerSpecial="pSpecial($event)" @monsterAttack="playerHealth -= $event" @mSpecial="mSpecial($event)" @mHeal="monsterHealth += $event"></app-commands>
        </div>
      </div>
 
      <div class="row">
        <div class="col">
          <app-log></app-log>
        </div>
      </div>
    </div>
    </div>
    
</template>

<script>
import Log from "./components/Log";
import Player from "./components/Player";
import Monster from "./components/Monster";
import Commands from "./components/Commands";
import { eventBus } from "./main";


export default {
  components:{
    appLog:Log,
    appPlayer:Player,
    appMonster:Monster,
    appCommands:Commands
  },
  data(){
    return {
    playerHealth:100,
     playerHeal:Number,
     playerSpecial:Number,
    playerAttack:Number,
     monsterAttack:Number,
      monsterHealth:100,
    }
  },
  methods:{
    mSpecial(event){
      this.monsterHealth -= event[1].target.value;
      this.playerHealth -= event[0].target.value;
    },
    pSpecial(event){
      console.log(event[0])
      this.playerHealth -= event[1];
      this.monsterHealth -= event[0];
      
    },
    pAttack(event){
      this.monsterHealth -= event;
      this.gameLog.push(`Player Attack: ${toString(event)}`);
      console.log(gameLog)
    }
  }
}
</script>

<style>

</style>
