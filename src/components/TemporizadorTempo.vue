<template>
     <div class="is-flex is-align-items-center is-justify-content-space-between">
    <CronometroContagem :tempoEmSegundos="tempoEmSegundos" />
    <button class="button" @click="iniciar" :disabled="cronometroRodando">
      <span class="icon">
        <i class="fas fa-play"></i>
      </span>
      <span>play</span>
    </button>
    <button class="button" @click="finalizar" :disabled="!cronometroRodando">
      <span class="icon">
        <i class="fas fa-stop"></i>
      </span>
      <span>stop</span>
    </button>
  </div>
</template>

<script lang="ts">

import {defineComponent} from "vue";
import CronometroContagem from './CronometroContagem.vue'

export default defineComponent({
   name: "temporizador-tempo",
   emits: ['aoTemporizadorFinalizado'],
   components:{
    CronometroContagem
   },
   data () {
    return {
        tempoEmSegundos: 0,
        cronometroContagem: 0,
        cronometroRodando: false
    }
   },
   methods: {
    iniciar () {
        //começar a contagem
        // 1 seg = 1000 ms
        this.cronometroRodando = true
        this.cronometroContagem = setInterval(() => {
            this.tempoEmSegundos +=1 
        }, 1000)
    },
    finalizar () {
        this.cronometroRodando = false
        clearInterval(this.cronometroContagem)
        this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
        this.tempoEmSegundos = 0
    }
   } 
});
</script>