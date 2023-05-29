<template>
  <div class="cronometro">
    <div class="horario">
        <strong >{{tempoDecorrido}}</strong>
    </div>
    <div class="acoes">
      <button class="botao play" @click="iniciarCronometro()" :disabled="estaCronometroRodando || habilitarCronometragem" >
        <span> play </span>
      </button>
      <button class="botao pause" @click="pausarCronometro()" :disabled="!estaCronometroRodando || habilitarCronometragem" >
        <span> pause </span>
      </button>
      <button class="botao stop"  @click="finalizarCronometro();" :disabled="!cronometroIniciado && (!estaCronometroRodando || habilitarCronometragem)" >
        <span> stop </span>
      </button>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent ({
    name: 'CronometroComponente',
    props: {
      habilitarCronometragem: {
        type: Boolean,
        required: false,
        default: true
      }
    },
    data() {
      return {
        tempoEmSegundos: 0 as number, 
        cronometro: 0 as any,
        estaCronometroRodando: false as boolean,
      }
    },
    computed: {
      tempoDecorrido(): string {
        return new Date(this.tempoEmSegundos * 1000).toISOString().substring(11, 19)
      },
      cronometroIniciado(): boolean {
        return this.tempoEmSegundos >= 1
      }
    },
    methods: {
      iniciarCronometro(): void {
        alert('iniciar cronogramas')
        this.estaCronometroRodando = true
        this.cronometro = setInterval(() => {
          this.tempoEmSegundos += 1
        }, 1000)        
      },
      pausarCronometro(): void {
        alert('pausar cronogramas')
        clearInterval(this.cronometro)
        this.estaCronometroRodando = false
      },
      async finalizarCronometro(): Promise<void> {
        await this.$emit('acao', this.tempoDecorrido)
        alert('finalizar cronogramas')
        this.tempoEmSegundos = 0
        clearInterval(this.cronometro)
        this.estaCronometroRodando = false
        console.log(this.tempoDecorrido)
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
.play:disabled {
  background: #e3e3e3;
  
}

.pause {
  background: #f0ab51;
}

.pause:disabled {
  background: #e3e3e3;
  
}

.stop {
  background: #f42f17;
}

.stop:disabled {
  background: #e3e3e3;
  
}
.horario {
  font-size: 2.5em;
}
</style>