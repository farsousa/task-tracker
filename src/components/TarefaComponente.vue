<template>
    <div class="tarefa">
        <h2> {{ descricao }} </h2>
        <p> {{ duracao }} </p>
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
    background-color: #f3f3f3;
    border-left: 8px solid black;
}

h2 {
    font-weight: bold;
}

p {
    font-size: 14px;
}

</style>