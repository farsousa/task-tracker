<template>
    <div class="tarefa">
        <h2> {{ descricao }}  </h2>
        <p> 
            <i class="material-icons">access_time</i>
            <span>{{ duracao }} </span>            
        </p>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent ({
    name: 'TarefaComponente',
    props: {
        descricao: {
            require: true,
            type: String,
            default: ''
        },
        duracao: {
            require: true,
            type: String,
            default: ''
        }
    }
})
</script>

<style scoped>
.tarefa {
    width: 100%;
    padding: 5px 20px;
    margin: 10px 0;
    background-color: #ffffff;
    border-left: 6px solid black;
}

h2 {
    font-weight: bold;
    font-size: 1.1em;
}

p {
    font-size: 14px;
    display: flex;
}

p span {
    margin-left: 10px;
}

</style>