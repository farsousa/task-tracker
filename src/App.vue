<template>
  <section class="pagina">
    <div class="temporizador">
      <input class="entrada-tarefa" type="text" placeholder="Qual tarefa você deseja iniciar?" v-model="tarefa.descricao" />     
      <CronometroComponente :habilitarCronometragem="!tarefa.descricao" @acao="registrarTarefa" />
    </div>
    
    <div class="tarefas">
      <h1>Tarefas</h1>
      <TarefaComponente v-for="(tarefa, index) in tarefas" :key="index" :descricao="tarefa.descricao" :duracao="tarefa.duracao" />
    </div>    
  </section>
</template>
<script lang="ts">

import { defineComponent } from 'vue'
import CronometroComponente from './components/CronometroComponente.vue'
import TarefaComponente from './components/TarefaComponente.vue'
import ITarefa from './interfaces/ITarefa'

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
        this.tarefas.push(this.tarefa)
        this.tarefa = {} as ITarefa 
      }else {
        alert("Preencha a tarefa executada!")
      }
      
    }

  }
});
</script>

<style scoped>

.pagina {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #ffffff;
  height: 100vh;
}
.entrada-tarefa {
  width: 100%;
  padding: 10px 30px;
  margin: 10px 0;
}

.temporizador, .tarefas {
  padding: 0 20px;
  width: 100%;
}

.tarefas h1 {
  text-align: center;
}
</style>
