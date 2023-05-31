<template>
  <section class="pagina">
    <div class="temporizador">
      <input class="entrada-tarefa" type="text" placeholder="Qual tarefa você deseja cronometrar?" v-model="tarefa.descricao" />     
      <CronometroComponente :estaPermitidoCronometragem="!tarefa.descricao" @acao="registrarTarefa" />
    </div>
    
    <div class="historico-tarefas">
      <h1>Histórico de Tarefas</h1>
      <i v-if="tarefas.length === 0">Você ainda não tem tarefas cronometradas...</i>
      <div v-for="(tarefa, index) in tarefas" :key="index">
        <p v-if="index === 0">{{ tarefa.data }}</p>
        <p v-if="index > 0 && tarefas[index - 1].data !== tarefa.data">{{ tarefa.data }}</p>
        <TarefaComponente  :descricao="tarefa.descricao" :duracao="tarefa.duracao" />
      </div>     
    </div> 
  </section>
</template>
<script lang="ts">

import { defineComponent } from 'vue'
import CronometroComponente from './components/CronometroComponente.vue'
import TarefaComponente from './components/TarefaComponente.vue'
import type ITarefa from './interfaces/ITarefa'

export default defineComponent ({
  name: 'App',
  components: {
    CronometroComponente,
    TarefaComponente,
  },
  data() {
    return {     
      tarefa: {} as ITarefa,
      tarefas: [] as ITarefa[]
    }
  },
  methods: {
    registrarTarefa(tempoDecorrido: string) {
      if(this.tarefa.descricao) {
        this.tarefa.duracao = tempoDecorrido
        this.tarefa.data = new Date().toLocaleString().substring(0,10)
        this.tarefas.push(this.tarefa)
        this.tarefa = {} as ITarefa 
      }else {
        alert("Preencha a tarefa executada!")
      }      
    },
    gerarNumeroAleatorio(min: number, max: number) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
    gerarDataAleatoria() {
      const ano = this.gerarNumeroAleatorio(2000, new Date().getFullYear());
      const mes = this.gerarNumeroAleatorio(0, 11);
      const dia = this.gerarNumeroAleatorio(1, new Date(ano, mes + 1, 0).getDate());
      return new Date(ano, mes, dia);
    }

  }
});
</script>

<style scoped>

.pagina {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  max-width: 600px;
  margin: auto;
  background-color: rgb(249, 249, 249);  
}
.entrada-tarefa {
  width: 100%;
  padding: 10px 30px;
  margin: 10px 0;
}

.temporizador, .historico-tarefas {
  padding: 0 20px;
  width: 100%;
}

.temporizador input {  
  outline: none;
  border: none;
  border-left: 6px solid black;
  background-color: #fff;
  height: 60px;
  font-size: 1em;
}

.temporizador input:focus {  
    outline: none;
    border: none;
    border-left: 6px solid black;
}

.historico-tarefas h1 {
  font-size: 1.9em;
  margin-top: 30px;
  font-weight: 700;
}

.historico-tarefas p {
  text-align: center;
  margin-top: 20px;
}

</style>
