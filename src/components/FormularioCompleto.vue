<template>
  <div class="box">
    <div class="columns">
      <div class="column is-8" role="form" aria-label="Formulário para criação de uma nova tarefa">
        <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao">
      </div>
      <div class="column">
        <TemporizadorFormulario @aoTemporizadorFinalizado="finalizarTarefa" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TemporizadorFormulario from './TemporizadorFormulario.vue';

export default defineComponent({
  name: "FormularioCompleto",
  emits: ['aoSalvarTarefa'],
  components: {
    TemporizadorFormulario,
  },
  data() {
    return {
      descricao: '',
    };
  },
  methods: {
    finalizarTarefa(tempoDecorrido: number): void {
      this.$emit('aoSalvarTarefa', { duracaoEmSegundos: tempoDecorrido, descricao: this.descricao });
      this.descricao = ''
    }
  }
})

</script>