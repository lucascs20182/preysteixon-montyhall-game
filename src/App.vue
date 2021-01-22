<template>
  <div id="app">
    
    <h1>
      O jogo do Preysteixon
      <span>Baseado no Problema de Monty Hall</span>
    </h1>

    <div class="form">
      
      <div v-if="!started">
        <label for="portsAmount">Quantas portas? </label>
        <input type="text" id="portsAmount" size="3"
          v-model.number="portsAmount">
      
      </div>
      
      <div v-if="!started">
        <label for="selectedPort">Qual porta é a premiada? </label>
        <input type="text" id="selectedPort" size="3"
          v-model.number="selectedPort">
      </div>
      
      <button v-if="!started" @click="started = true">Iniciar</button>
      <button v-if="started" @click="started = false">Reiniciar</button>
    </div>

    <div class="doors" v-if="started">
      <div v-for="i in portsAmount" :key="i">
        <Door :hasGift="i === selectedPort" :number="i" />
      </div>
    </div>

  </div>
</template>

<script>
    import Door from './components/Door'

    export default {
        name: 'App',
        components: { Door },
        
        data: function() {
            return {
                started: false,
                portsAmount: 3,
                selectedPort: null
            }
        }
    }
</script>

<style>
    * {
        box-sizing: border-box;
        font-family: 'Montserrat', sans-serif;
    }

    body {
        color: #fff;
        background: linear-gradient(to right,
            rgb(21, 153, 87), rgb(21, 87, 153))
    }

    #app {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    #app h1 {
        background-color: #0004;
        border: 1px solid #000;
        padding: 20px;
    }
  
    #app h1 span {
        font-size: 1.3rem;
        padding-top: 5px;

        display: flex;
        justify-content: center;
    }

    .form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        
        margin-bottom: 40px;
    }

    .form, .form input, .form button {
        margin-bottom: 10px;
        font-size: 2rem;
    }

    .doors {
        align-self: stretch;

        display: flex;
        justify-content: space-around;
        flex-wrap: wrap;
    }
</style>
