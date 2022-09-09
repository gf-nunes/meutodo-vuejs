<template>
  <div id="app">
    <nav class="orange darken-2">
      <div class="nav-wrapper"></div>
    </nav>
    <img alt="Vue logo" src="../assets/logo.png" width="32" />
    <!-- Lista -->
    <div v-show="exibir.lista" style="padding 20px">
      <button @click="mostrarCadastro">Adicionar</button>
      <TarefaList
        msg="Welcome to Your Vue.js App"
        :tasks="listaDeTarefas"
      ></TarefaList>
    </div>
    <!-- FORM -->
    <div v-show="exibir.form">
      <tarefa-form
        :titulo="form.titulo"
        @salvarClick="recebiSalvar"
      ></tarefa-form>
    </div>
  </div>
</template>
<script>
import TasksApi from "../TasksApi.js"
import TarefaList from "../components/TarefaList.vue"
import TarefaForm from "../components/TarefaForm.vue"

export default {
  components: {
    TarefaList,
    TarefaForm,
  },
  data: () => {
    return {
      listaDeTarefas: [],
      exibir: {
        lista: true,
        form: false,
      },
      form: {
        titulo: "Cadastrar Tarefa",
      },
    }
  },
  methods: {
    listarTarefas() {
      TasksApi.getTasks((data) => {
        this.listaDeTarefas = data
      })
    },
    mostrarCadastro() {
      this.exibir.form = true
      this.exibir.lista = false
    },
    recebiSalvar(novaTarefa) {
      console.log("recebi o evento", novaTarefa)
      TasksApi.createTask(novaTarefa, () => {
        console.log("salvei")
        this.listarTarefas()
        this.exibir.form = false
        this.exibir.lista = true
      })
    },
  },
  created() {
    this.listarDeTarefas()
  },
}
</script>
<style></style>
