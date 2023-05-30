<template>
  <div class="cronometro">
    <strong >{{tempoDecorrido}}</strong>
    <button class="play" @click="iniciarCronometro()" >
      <span> PLAY </span>
    </button>
    <button class="pause" @click="pausarCronometro()" >
      <span> PAUSE </span>
    </button>
    <button class="stop"  @click="finalizarCronometro();" >
      <span> STOP </span>
    </button>
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
        if(this.estaCronometroRodando || this.habilitarCronometragem) {
          alert('informe a tarefa')
        }else {
          alert('iniciar cronogramas')
          this.estaCronometroRodando = true
          this.cronometro = setInterval(() => {
            this.tempoEmSegundos += 1
          }, 1000)     
          
        }          
      },
      pausarCronometro(): void {
        if(!this.estaCronometroRodando || this.habilitarCronometragem) {
          alert('Não pode pausar, já que nem começou a cronometragem')
        } else {
          alert('pausar cronogramas')
          clearInterval(this.cronometro)
          this.estaCronometroRodando = false          
        }
        
      },
      async finalizarCronometro(): Promise<void> {
        if(!this.cronometroIniciado && (!this.estaCronometroRodando || this.habilitarCronometragem)) {
          alert('Não finalizado')
        }else {
          await this.$emit('acao', this.tempoDecorrido)
          alert('finalizar cronogramas')
          this.tempoEmSegundos = 0
          clearInterval(this.cronometro)
          this.estaCronometroRodando = false
          console.log(this.tempoDecorrido)         
        }
        
      }
    }
})
</script>

<style scoped>
.cronometro {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  align-items: center;
  width: 100%;
  background-color: #c15c5c;
}

.cronometro strong {
  font-size: 3em;
  font-weight: 700;
  color: white;
}

.cronometro span {
  font-size: 3em;
  font-weight: 700;
}

.cronometro button {
  border-radius: 6px;
  border: 0;
  color: white;
  width: 90%;
  font-size: 0.4em;
  margin: 10px 0;
  padding: 10px 0;
}

.cronometro button:disabled {
  background: #e3e3e3;
  color: #000;
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

</style>