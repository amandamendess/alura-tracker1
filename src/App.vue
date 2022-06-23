<template>
  <main class="columns is-gapless is-multiline" :class="{'modo-escuro': modoEscuroAtivo}">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioTempo @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <TarefaLista v-for= "(tarefalista, index) in tarefas" :key="index" :tarefalista="tarefalista"/>
        <BoxDescricao v-if="listaEstaVazia">
        Nenhuma tarefa realizada hoje.
      </BoxDescricao>
      </div> 
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue'
import FormularioTempo from './components/FormularioTempo.vue'
import TarefaLista from './components/TarefaLista.vue'
import BoxDescricao from './components/BoxDescricao.vue'
import ITarefa from './interfaces/ITarefa'

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioTempo,
    TarefaLista,
    BoxDescricao
  },
  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed:{
    listaEstaVazia () : boolean {
      return this.tarefas.length === 0
    }
  },
  methods : {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo : boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
});
</script>

<style>
.lista {
  padding: 1.25rem;
}
main {
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>

