<template>
<div class="container">
    <div v-if="!entrar" class="nav-centro" >
      <div class="login">
         <form class="registrar">
           <h1 class="texto">LOGIN</h1>
         <input type="text" class="input" v-model="nome" placeholder="Nome">
         <input type="text" class="input" v-model="email" placeholder="Email">
         <button v-on:click="botaoEntrar" class="botao-entrar">ENTRAR</button>
        </form>
      </div>
    </div>
    <div v-if="entrar" class="nav-esquerda">
        <h1>Pessoas Online</h1>
    </div>
    <div v-if="entrar" class="nav-direita">
    <div  class="box-mensagens"> 
      <div  class="mensagens"> 
      <div v-for="mensagem in mensagens" :key="mensagem.id">
       
        <b>
          {{mensagem.usuario}}
        </b>
        : {{mensagem.texto}}

      </div>
      </div>   
    </div>
    </div>
      <div v-if="entrar" class="nav-pe">
        <textarea v-model="texto" v-on:keyup.enter="enviarMsg" class="area-texto" placeholder="Digite aqui...">
        </textarea>
      </div>
    </div>
</template>

<script>
import io from 'socket.io-client';
export default {
  name: 'Chat',
  data(){
      return {
        entrar: false,
        erro: false,
        nome: "",
        email: "",
        texto: "",
        mensagens: [],
      }
  },
  methods: {
    botaoEntrar(){

      this.entrar = true;
      this.socketInstance = io("http://localhost:3000");
      this.socketInstance.on(
        "mensagem:recebida", (data) => {
          this.mensagens = this.mensagens.concat(data);
        }
      );

  },
    enviarMsg(){
      this.addMsg();
      this.texto = "";
    },
    addMsg(){
      const mensagem = {
        id: new Date().getTime(),
        texto: this.texto,
        usuario: this.nome
      };
      this.mensagens = this.mensagens.concat(mensagem);
      this.socketInstance.emit('mensagem', mensagem);
    }
  }
  
}
</script>

<style>
.container{
  position: relative;
  display: grid;
  grid-template-areas:  "e d" "e p" ;
  grid-template-columns: 1fr 5fr ;
  grid-template-rows: 6fr 1fr;
  width: 98vw;
  height: 80vh;
}
.nav-centro{
  width: 98vw;
  height: 70vh;
  align-items: center;
  display: flex;
  justify-content: center;

  }
  .login{
    margin: 0 auto;
    width: 400px;
    height: 360px;
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
}
.input{
  width: 350px;
  padding: 20px;
  margin: 15px;
  display: flex;
  flex-direction: column;
  border: none;
  border-radius: 4px;
  background: #f1f1f1;
}
.botao-entrar{
  padding: 20px;
  width: 390px;
  margin-top: 40px;
  background: #4BC7EE;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-family: sans-serif;
  font-weight: bold;
  color: #fff;
}
.texto{
  margin-bottom: 40px;
}
.nav-esquerda{
  background: #F0F0;
  grid-area: e;
}
.nav-direita{
  background: #F0F0F0;
  text-align: initial;
  padding: 20px;
  overflow: auto;
  grid-area: d;
}
.nav-pe{
  background: #00f;
  grid-area: p;
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  justify-content: center;
}
.area-texto {
  bottom: 0;
  width: 100%;
  height: 100%;
  justify-content: center;
  padding: 10px;
  box-sizing: border-box; 
}

</style>