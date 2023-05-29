<template>
    <button class="botao" :style="{ backgroundColor: cor }" @click="$emit('acao')" :disabled="desativado" >
        <span>{{ nome }}</span>
    </button>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent ({
    name: 'BotaoComponente',
    props: {
        nome: {
            required: true,
            type: String,
            default: ''
        },
        cor: {
            required: true,
            type: String,
            default: 'black'
        },
        desativado: {
            required: true,
            type: Boolean,
            default: false
        }
    },
})
</script>

<style scoped>
.botao {
  border-radius: 4px;
  border: 0;
  box-shadow: 0px 0px 3px 0px;
  height: 30px;
  width: 90px;
  color: white;
  margin: 10px ;
}
</style>