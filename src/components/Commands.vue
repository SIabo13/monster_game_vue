<template>


<div>
    <div  v-if="startGame">
        <h1 class="text-center">{{ summary }}</h1>
        
        <div class="d-flex p-5 border m-5 ">
        <button :disabled="gameOver" @click="playerAttack" class="btn btn-danger">Attack</button>
        <button :disabled="gameOver" @click="playerSpecial" class="btn btn-warning">Special</button>
        <button :disabled="gameOver" @click="playerHeal" class="btn btn-success">Heal</button>
        <button @click="startGame = !startGame" class="btn btn-dark">Quit</button>
    </div>
    </div>
    
<div v-if="!startGame">
        <h1 class="text-center">Begin Your Epic Battle</h1>
<div class="border  p-5 m-5">
    <button @click="start" class="btn btn-success d-block m-auto m-4">Start Game</button>
</div>
</div>


</div>



    
</template>
<script>
import { eventBus } from '../main';


export default {
    props:['pHealth','mHealth'],
    data(){
        return {
            startGame:false,
            gameOver:false,
            playerAtkDamage:0,
            heal:0,
            special:0,
            mAttack:0,
            mHeal:0,
            mSpecial:0,
            summary:'Defeat Your Enemy',
            sDamage:0,
            gameValue:{
                special:45,
                specialDamage:25,
                attack:20,
                heal:35
            },
            battleLog: []
            // enemystrategy:{

            // }
            
        }
    },
    methods:{
        start(){
            this.startGame = !this.startGame;
            if(this.pHealth <= 0 || this.mHealth <= 0){
                this.$emit("pReset",100);
                this.$emit("mReset",100);
                this.gameOver = false;
            }
            
        },
        playerAttack(){
        console.log("Attack is working")
        this.playerAtkDamage = Math.floor(Math.random() * this.gameValue.attack);
        console.log(this.playerAtkDamage)
        console.log(this.mHealth)
        console.log(this.pHealth)
        this.$emit("playerAttack",this.playerAtkDamage);
        this.monsterLogic();
        this.endGame();
        
    },
        playerHeal(){
                if(true){
                    console.log("Player Heal");
                    this.heal = Math.floor(Math.random() * this.gameValue.heal);
                    console.log(this.heal)
                    this.$emit("playerHeal",this.heal);

                    this.monsterLogic();

                     this.endGame();
                }
            

        },
        playerSpecial(){
            console.log("Player Special")
            this.special = Math.floor(Math.random() * this.gameValue.special);
            this.sDamage = Math.floor(Math.random() * this.gameValue.specialDamage);
            let special = [this.special,this.sDamage];
            this.$emit("playerSpecial",special);

            this.monsterLogic();

             this.endGame();

        },
        monsterAttack(){
            this.mAttack = Math.floor(Math.random() * this.gameValue.attack);
            console.log("The monster attack is:" + this.mAttack);
            this.$emit("monsterAttack",this.mAttack)
        },
        monsterHeal(){
          this.mHeal += Math.floor(Math.random() * this.gameValue.heal);
          this.$emit("mHeal",this.mHeal)

        },
        monsterSpecial(){
          this.mSpecial = Math.floor(Math.random() * this.gameValue.special);
          this.mHealth -= Math.floor(Math.random() * this.gameValue.specialDamage);
          let special = [this.mHealth,this.mSpecial]
          this.$emit('mSpecialAttack', special);


        },
        monsterLogic(){
            if(this.mHealth > 70){
                this.monsterAttack();
            }else if(this.mHealth <= 35){
                this.monsterHeal();
            }else if(this.pHealth <= 30){
                this.monsterSpecial();
            }else if(this.pHealth > 50 && this.mHealth < 50){
                this.monsterHeal();
            }else if(this.pHealth <= 30 && this.mHealth <= 30){
                this.monsterSpecial();
            }
        },
        endGame(){
            if(this.pHealth <= 0){
              this.summary = "Monster wins";
              this.gameOver = true;  
             
            }else if(this.mHealth <= 0){
                this.summary = "You win!!!";
                this.gameOver = true;
            }

            
        },
        init(){
            //Controls player and monster turns and events
        }


    }
   
}
</script>

<style scoped>
div{
    justify-content: center;
}
button{
    margin:15px;
}
</style>