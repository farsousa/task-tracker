<template>
  <div class="cronometro">
    <div class="tempo">
      <strong >{{tempoDecorrido}}</strong>
    </div>    
    <div class="acoes">      
      <i class="material-icons play" v-show="!estaRodandoCronometro" @click="iniciarCronometro()">play_arrow</i>
      <i class="material-icons pause" v-show="estaRodandoCronometro"  @click="pausarCronometro()">pause</i>
      <i class="material-icons stop" v-show="foiIniciadoCronometro" @click="finalizarCronometro();">stop</i>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent ({
    name: 'CronometroComponente',
    props: {
      estaPermitidoCronometragem: {
        type: Boolean,
        required: false,
        default: true
      }
    },
    data() {
      return {
        tempoEmSegundos: 0 as number, 
        cronometro: 0 as any,
        estaRodandoCronometro: false as boolean,
      }
    },
    computed: {
      tempoDecorrido(): string {
        return new Date(this.tempoEmSegundos * 1000).toISOString().substring(11, 19)
      },
      foiIniciadoCronometro(): boolean {
        return this.tempoEmSegundos > 0
      }
    },
    methods: {
      iniciarCronometro(): void {
        if(this.estaRodandoCronometro || this.estaPermitidoCronometragem) {
          alert('informe a tarefa')
        }else {
          this.estaRodandoCronometro = true
          this.cronometro = setInterval(() => {
            this.tempoEmSegundos += 1
          }, 1000)     
          
        }          
      },
      pausarCronometro(): void {
        if(!this.estaRodandoCronometro || this.estaPermitidoCronometragem) {
          
        } else {
          clearInterval(this.cronometro)
          this.estaRodandoCronometro = false          
        }
        
      },
      async finalizarCronometro(): Promise<void> {
        if(!this.foiIniciadoCronometro && (!this.estaRodandoCronometro || this.estaPermitidoCronometragem)) {
         
        }else {
          await this.$emit('acao', this.tempoDecorrido)
          this.tempoEmSegundos = 0
          clearInterval(this.cronometro)
          this.estaRodandoCronometro = false
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
}

.cronometro .tempo strong {
  font-size: 3em;
  font-weight: 700;
  color: #000000;
}

.cronometro .acoes {
  display: flex;
  width: 100%;
}

.cronometro .acoes i {
  font-size: 3em;
  font-weight: 700;
  color: #ffffff;
  flex-grow: 1;
  text-align: center;
  cursor: pointer;
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

.play:hover {
  background: #2c5b22;
}

.pause {
  background: #f0ab51;
}

.pause:hover {
  background: #c48c42;
}

.stop {
  background: #f42f17;
}

.stop:hover {
  background: #a62110;
}

</style>