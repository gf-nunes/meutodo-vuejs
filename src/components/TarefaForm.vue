<template>
  <div>
    <h2>{{ titulo }}</h2>
    <input
      type="text"
      name="title"
      id="title"
      placeholder="Entre com a tarefa"
      v-model="form.title"
    />
    <input
      type="text"
      name="title"
      v-model="form.projetc"
      placeholder="Entre com um projeto"
    />
    <button @click="salvarTarefa">Salvar</button>
  </div>
</template>

<script>
export default {
  props: ["titulo"],
  data: () => {
    return {
      form: {
        tittle: "",
        project: "",
      },
    };
  },
  methods: {
    salvarTarefa() {
      const novaTarefa = {
        title: this.form.title,
        project: this.form.project,
        date: new Date().toLocaleDateString("pt"),
      };
      this.$emit("salvarClick", novaTarefa);
    },
  },
};
</script>
