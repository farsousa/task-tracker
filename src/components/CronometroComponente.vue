<template>
  <div class="cronometro">
    <div class="horario">
        <strong >{{tempoDecorrido}}</strong>
    </div>
    <div class="acoes">
      <button class="botao play" @click="iniciarCronometro()" :disabled="estaCronometroRodando" >
        <span> play </span>
      </button>
      <button class="botao pause" @click="pausarCronometro()" :disabled="!estaCronometroRodando" >
        <span> pause </span>
      </button>
      <button class="botao stop"  @click="finalizarCronometro()" :disabled="false" >
        <span> stop </span>
      </button>
    </div>
  </div>
</template>
<script>
import { defineComponent } from 'vue'

export default defineComponent ({
    name: 'CronometroComponente',
    data() {
      return {
        tempoEmSegundos: 0,
        cronometro: 0,
        estaCronometroRodando: false,
      }
    },
    computed: {
      tempoDecorrido() {
        return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11, 8)
      }
    },
    methods: {
      iniciarCronometro() {
        alert('iniciar cronogramas')
        this.estaCronometroRodando = true
        this.cronometro = setInterval(() => {
          this.tempoEmSegundos += 1
        }, 1000)
        
      },
      pausarCronometro() {
        alert('pausar cronogramas')
        clearInterval(this.cronometro)
        this.estaCronometroRodando = false
      },
      finalizarCronometro() {
        alert('finalizar cronogramas')
        this.tempoEmSegundos = 0
        clearInterval(this.cronometro)
        this.estaCronometroRodando = false
      }
    }
})
</script>

<style scoped>
.cronometro {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    max-width: 350px;
}

.botao {
  border-radius: 4px;
  border: 0;
  box-shadow: 0px 0px 3px 0px;
  height: 30px;
  width: 90px;
  color: white;
  margin: 10px ;
}

.play {
  background: #3c7b2f;
}

.pause {
  background: #f0ab51;
}

.stop {
  background: #f42f17;
}
.horario {
  font-size: 2.5em;
}
</style>