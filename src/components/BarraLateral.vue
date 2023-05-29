<template>
    <header>
        <img id="logo" src="../assets/logo-nova.png" alt="" />
    </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent ({
    name: 'BarraLateral'
})
</script>

<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 1rem;
  background: #ffffff;
  width: 100%;
  height: 100vh;
  box-shadow: 0px 0px 3px 0px;
}

#logo {
    max-width: 200px;
    margin: 0;
}

@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>