<template>


<div>
    <div  v-if="startGame">
        <h1 class="text-center">Defeat Your Enemy</h1>
        <div class="d-flex p-5 border m-5 ">
        <button @click="playerAttack" class="btn btn-danger">Attack</button>
        <button @click="playerSpecial" class="btn btn-warning">Special</button>
        <button @click="playerHeal" class="btn btn-success">Heal</button>
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
export default {
    props:['pHealth','mHealth'],
    data(){
        return {
            startGame:false,
            playerAtkDamage:0,
            heal:0,
            special:0,
        }
    },
    methods:{
        start(){
            this.startGame = !this.startGame;
            if(this.pHealth <= 0 || this.mHealth <= 0){
                this.$emit("pReset",100);
                this.$emit("mReset",100);
            }
            
        },
        playerAttack(){
        console.log("Attack is working")
        this.playerAtkDamage = Math.floor(Math.random() * 25);
        console.log(this.playerAtkDamage)
        console.log(this.mHealth)
        console.log(this.pHealth)
        this.$emit("playerAttack",this.playerAtkDamage);
        this.endGame();
        
    },
        playerHeal(){
            console.log("Player Heal");
            this.heal = Math.floor(Math.random() * 25);
            console.log(this.heal)
            this.$emit("playerHeal",this.heal);

        },
        playerSpecial(){
            console.log("Player Special")
            this.special = Math.floor(Math.random() * 25);
            console.log(this.special)
            this.$emit("playerSpecial",this.special);

        },
        monsterAttack(){

        },
        monsterHeal(){

        },
        monsterSpecial(){

        },
        endGame(){
            if(this.mHealth <= 0 || this.pHealth <= 0){
                this.startGame = !this.startGame;
            }
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