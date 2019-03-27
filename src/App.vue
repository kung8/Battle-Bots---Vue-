<template>
  <div id="app">
    <h1>Battle Bots</h1>
    <h1 @click='showCreate'>Create</h1>
    <h1 @click='showCollection'>Collection</h1>
    
    <section v-if='showForm'>
      <p v-if='selected1'>Bot #1: Select a bot below</p><p v-else>Bot #1:{{battle[0].name}}</p>
      <p v-if='selected2'>Bot #2: Select a bot below</p><p v-else>Bot #2:{{battle[1].name}}</p>
      <button @click='fight'>Battle</button>
      <button @click='clearBattle'>Clear</button>
      <hr>
      <list v-for="(bot,i) in allBots" :key='i' :bot='bot' :index='i' :retire='retire' :select='select'/>
    </section>

    <section v-else>
      <h1>Create Bot</h1>
        <p>Bot Name:<input type="text" v-model='name'></p>
        <p>Attack Value:<input type="number" v-model='attack'></p>
        <p>Health Value:<input type="number" v-model='health'></p>
        <button @click='clear'>Clear</button>
        <button @click='addBot'>Add</button>
    </section>
  </div>
</template>

<script>
import List from './components/List';

export default {
  name: 'app',
  data:function(){
    return{
      showForm:true,
      name:'',
      attack:'',
      health:'',
      allBots:[],
      selected1:true,
      selected2:true,
      battle:[]
    }
  },
  components: {
    List:List
  },
  methods:{
    showCreate(){
      this.showForm = false
    },

    showCollection(){
      this.showForm = true
    },

    clear(){
      this.name = '';
      this.health = 0;
      this.attack = 0;
    },

    addBot(){
      const bot = {name:this.name,attack:this.attack,health:this.health}
      this.allBots.push(bot)
      this.clear()
      this.showForm=true
    },

    retire(i){
      this.allBots = this.allBots.filter((bot,index)=>{
        return index !==i
      })
    },

    select(bot){
      // console.log('hit!');
      // console.log('bot', bot);
      if(!this.battle[1]){
        this.selected1 = false;
        // console.log('before battle',this.battle);
        if(this.battle[0]){
          this.selected2 = false
          this.battle.push(bot);
        }
        this.battle.push(bot);
        
        // console.log('after battle',this.battle);
      } else {
        alert('Too many bots!');
      }
    },

    clearBattle(){
      this.battle = [];
      this.selected1 = true
      this.selected2 = true
    },   
  
    fight(){
      console.log('hit');
      console.log(this.battle[0].health, this.battle[0].attack)
      console.log(this.battle[1].health, this.battle[1].attack)
      let bot1 = this.battle[0]
      let bot2 = this.battle[1]
      // if(bot1.health - bot2.attack % 0){
      let botone = parseInt(bot1.health) / parseInt(bot2.attack);
      let bottwo = parseInt(bot2.health) / parseInt(bot1.attack);
      parseInt(botone)
      parseInt(bottwo)
      console.log(botone,bottwo)
      if(botone > bottwo){
        alert(`${this.battle[0].name} wins`)
      }  else if (bottwo > botone){
        alert(`${this.battle[1].name} wins`)
      } else {
        alert("It's a draw!")
      }
      this.battle = [];
      this.selected1 = true;
      this.selected2 = true;
    }
  },

}
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
