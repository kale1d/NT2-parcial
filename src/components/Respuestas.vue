<template lang="html">

  <section class="respuestas">
    <div class="jumbotron">
      <table class="table table-dark">
        <thead>
          <tr>
            <th scope="col">Pregunta</th>
            <th scope="col">Respuesta</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(resp, i) in respuestas" :key="i">
            <th scope="row">{{ resp.pregunta }}</th>
            <th scope="row">{{ resp.respuesta }}</th>
          </tr>
        </tbody>
      </table>
    </div>
    <p>Aclaración: Si bien la función principal de router es la de conectar con una url, también se pueden pasar por
      query params data recibida</p>
  </section>
</template>

<script lang="js">

export default {
  name: 'respuestas-component',
  props: [],
  mounted() {
    this.getResponses();
  },
  data() {
    return {
      respuestas: [],
    }
  },
  methods: {
    getResponses() {
      const r1 = { pregunta: 1, respuesta: '[d]' };
      const r2 = { pregunta: 2, respuesta: '[c]' };
      const r3 = { pregunta: 3, respuesta: '[b, d]' };
      this.respuestas.push(r1, r2, r3);
    }
  },
  computed: {

  }
}


</script>

<style scoped lang="css">
.jumbotron {
  height: 100vh;
  background-color: #ECE3FC;
}
</style>
