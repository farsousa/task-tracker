<template>
  <section class="pagina">
    <section class="menu">
      <BarraLateral />
    </section>
    <section class="conteudo">
      <div class="entrada-tarefa">
        <input type="text" placeholder="Qual tarefa você deseja iniciar?" v-model="tarefa.descricao" />     
        <CronometroComponente :habilitarCronometragem="!tarefa.descricao" @acao="registrarTarefa" />
      </div>
      <div class="lista-tarefa">        
        {{ tarefas }}
      </div>
    </section>    
  </section>
</template>
<script lang="ts">

import { defineComponent } from 'vue'
import BarraLateral from './components/BarraLateral.vue'
import CronometroComponente from './components/CronometroComponente.vue'

type Tarefa = {
  descricao: string;
  duracao: string;
}
export default defineComponent ({
  name: 'App',
  components: {
    BarraLateral,
    CronometroComponente,
  },
  data() {
    return {     
      tarefa: {} as Tarefa,
      tarefas: [] as Tarefa[]
    }
  },
  methods: {
    registrarTarefa(tempoDecorrido: string) {
      if(this.tarefa.descricao) {
        this.tarefa.duracao = tempoDecorrido
        this.tarefas.push(this.tarefa)
        this.tarefa = {} as Tarefa 
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
}

.menu {
  width: 20%;
}

.conteudo {
  width: 80%;  
  padding: 40px 0;
}

.entrada-tarefa {
  width: 400px;
  margin: auto;
  display: flex;
}

.entrada-tarefa input {
  width: 100%;
  padding: 10px 20px;
}
</style>
