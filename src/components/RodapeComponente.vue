<template>
  <footer class="rodape">
    <i class="material-icons item">home</i>
    <i class="material-icons item middle">access_time</i>
    <i class="material-icons item">assignment</i>
  </footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent ({
  name: 'RodapeComponente'
})
</script>

<style scoped>
.rodape {
  width: 100%;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px 0;
  box-shadow: 0 0 2px 0px;
}

.item {
  flex-grow: 1;
  text-align: center;
}

.item:hover {
  background-color: bisque;
}

.middle {
  font-size: 3em;
}
</style>