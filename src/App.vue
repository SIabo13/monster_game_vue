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
          <app-commands @pReset="playerHeal = $event" @mReset="monsterHealth = $event" :pHealth="playerHealth" :mHealth="monsterHealth"  @playerAttack="monsterHealth -= $event" @playerHeal="playerHealth += $event" @playerSpecial="monsterHealth -= $event"></app-commands>
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
import Commands from "./components/Commands"


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
  }
 
}
</script>

<style>

</style>
