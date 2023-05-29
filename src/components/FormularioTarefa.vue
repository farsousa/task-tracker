<template>
  <div class="form-task">
    <div class="input">
      <input type="text" placeholder="Qual tarefa você deseja iniciar?" />
    </div>
    <div class="actions">
      <section class="timer">
        <strong >{{tempoDecorrido}}</strong>
      </section>
      <section class="buttons">
        <button class="play" @click="iniciarCronometro">
          <span>play</span>
        </button>
        <button class="pause" @click="pausarCronometro">
          <span>pause</span>
        </button>
        <button class="stop" @click="finalizarCronometro">
          <span>stop</span>
        </button>
      </section>      
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent ({
    name: 'FormularioTarefa',
    data() {
      return {
        tempoEmSegundos: 0,
        cronometro: 0
      }
    },
    computed: {
      tempoDecorrido(): string {
        return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11, 8)
      }
    },
    methods: {
      iniciarCronometro() {
        this.cronometro = setInterval(() => {
          this.tempoEmSegundos += 1
        }, 1000)
      },
      pausarCronometro() {
        clearInterval(this.cronometro)
      },
      finalizarCronometro() {
        alert('finalizar cronogramas')
      }
    }
})
</script>

<style scoped>
.form-task {
  display: flex;
  align-items: center;
  padding: 20px 40px;
  justify-content: space-between;
}

.form-task .input {
  flex-grow: 5;
}

.form-task .input input[type="text"] {
  width: 100%;
  padding: 10px 30px;
  border: 0px;
  border-radius: 4px;
  box-shadow: 0px 0px 3px 0px;
}

.form-task .input input[type="text"]:hover,
.form-task .input input[type="text"]:focus{
  background-color: #ffffff !important;
  border-color: #ccc !important;
  outline: 0 !important;
}

.form-task .actions {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-task .actions .timer {
  font-size: 2.5em;
}

.form-task .actions .buttons {
  display: flex;
  width: 70%;
  justify-content: space-around;
}

.form-task .actions button {
  border-radius: 4px;
  border: 0;
  box-shadow: 0px 0px 3px 0px;
}

.form-task .actions .play {
  height: 30px;
  width: 90px;
  background: #3c7b2f;
  color: white;
  
}

.form-task .actions .play:hover {
  background: #78b968;
}

.form-task .actions .pause {
  height: 30px;
  width: 90px;  
  background: #f0ab51;
  color: white;
}

.form-task .actions .pause:hover {
  height: 30px;
  width: 90px;  
  background: #f8d581;
  color: white;
}

.form-task .actions .stop {
  height: 30px;
  width: 90px;  
  background: #b6170c;
  color: white;
}

.form-task .actions .stop:hover {
  height: 30px;
  width: 90px;  
  background: #f42f17;
  color: white;
}


</style>