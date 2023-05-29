<template>
  <section class="pagina">
    <section class="menu">
      <BarraLateral />
    </section>
    <section class="conteudo">
      <div class="entrada-atividade">
        <input type="text" placeholder="Qual tarefa você deseja iniciar?" />     
        <CronometroComponente />
      </div>
    </section>    
  </section>
</template>
<script>

import { defineComponent } from 'vue'
import BarraLateral from './components/BarraLateral.vue'
import CronometroComponente from './components/CronometroComponente.vue'

export default defineComponent ({
  name: 'App',
  components: {
    BarraLateral,
    CronometroComponente
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

.entrada-atividade {
  width: 400px;
  margin: auto;
}

.entrada-atividade input {
  width: 100%;
  padding: 10px 20px;
}
</style>
