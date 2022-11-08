<template>
  <section class="src-componentes-choice">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <br />

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Numero de pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr v-for="(dato, index) in preguntas" :key="index">
            <td>{{ dato.numero }}</td>
            <td>{{ dato.respuestas }}</td>
          </tr>
        </table>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-choice",
  props: [],
  mounted() {},
  data() {
    return {
      preguntas: [
        { numero: 1, respuestas: ['b','d'] },
        { numero: 2, respuestas: ['a','b','c']  },
        { numero: 3, respuestas: ['b','e'] },
      ],
    };
  },
  methods: {},
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: crimson;
  color: black;
}

hr {
  background-color: #bbb;
}
</style>
