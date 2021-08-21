<template>
  <div id="app">
   <img src="./assets/cronometro.png" class="imagem">
   <a class="timer">{{numero}}</a>
  
        <div class="areaBtn">
          <button class="botao" @click="vai">{{botao}}</button>
          <button class="botao" @click="limpar"> LIMPAR</button>
        </div>
        <div class="lista" v-show="historico.length > 0">
          <ul>
            <li v-for="item in historico" :key="item"> Você fez uma Pausa em : {{item}} </li>
            
          </ul>
          <button @click="historico = []">Limpar Histórico</button>
        </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      numero: 0,
      botao: 'Vai',
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historico: []
    }
  },
  methods:{
    vai(){
      if(this.timer !== null){
          //Aqui Significa que tem algo rodando no cronometro
          clearInterval(this.timer);
          this.timer = null;
          this.botao = 'VAI';
          if(this.ss !==0){
            this.historico.push(this.numero);

          }
      }else{
        //Aqui não tem nada no cronômetro, irá começar a rodar
        this.timer = setInterval(()=> {
          this.rodarTime();
        }, 100); //Aqui temos 1 segundo;
        this.botao = "PAUSAR"
      }
      
    },
    limpar(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
      }
      this.ss =0;
      this.mm =0;
      this.hh =0;
      this.numero =0;
      this.botao = 'VAI';
      this.historico =[];

    },
    rodarTime(){
      this.ss ++;
      if(this.ss == 59){

        //Aqui chegamos em 59 segundos....
        this.ss =0;
        this.mm ++;
      }

      if(this.mm == 59){
        //Aqui chegou até 59 minutos...
        this.mm =0;
        this.hh ++;
      }

      let relogio = (this.hh < 10 ? '0'+ this.hh : this.hh) + ':' +(this.mm < 10 ? '0'+ this.mm : this.mm) + ':' + (this.ss < 10 ? '0'+this.ss : this.ss);

      return this.numero = relogio;

    }
  }
}
</script>

<style>
#app{
  display:flex;
  width: 100%;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.imagem{
  width: 420px;
  height: 420px;
  padding-top: 100px;
}
.timer{
  color: white;
  font-size: 70px;
  margin-top: -220px;
}
.areaBtn{
  margin-top: 155px;
  display: flex;
}
.botao{
  -webkit-user-select: none;
  -moz-user-select: none;
  width: 150px;
  font-size: 20px;
  border: 0;
  border-radius: 5px;
  text-align: center;
  margin-left: 15px;
  margin-right: 15px;
  padding: 6px;
  cursor: pointer;
}
.botao:hover{
  opacity: 0.8;
  transition: all 0.58;
}
ul{
   text-align: center;
   padding: 0px;
}

ul li{
  margin-top: 4px;
  padding: 15px;
  background-color: rgb(70,70,70);
  list-style: none;
  color:white;
  font-size: 12px;
  border-radius: 6px;
}
.lista button{
  cursor: pointer;
  border: 0;
  background-color: darkseagreen;
  padding: 8px;
  border-radius: 5px;
  margin-bottom: 12px;
}
</style>
