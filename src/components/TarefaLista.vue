<template>
    <BoxDescricao>
        <div class="columns">
            <div class="column is-7">{{tarefalista.descricao || 'Tarefa sem descrição'}}</div>
            <div class="column">
                <CronometroContagem :tempoEmSegundos ="tarefalista.duracaoEmSegundos" />
            </div>
        </div>
    </BoxDescricao>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import CronometroContagem from './CronometroContagem.vue'
import ITarefa from '../interfaces/ITarefa'
import BoxDescricao from './BoxDescricao.vue'

export default defineComponent({
    name: "tarefa-lista",
    components: {
        CronometroContagem,
        BoxDescricao
    },
    props: {
        tarefalista: {
            type: Object as PropType <ITarefa>,
            required: true
        }
    }
});
</script>

