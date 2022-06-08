<template>
  <section class="src-componentes-respuestas">
    <div class="jumbotron">
      <h2><i>Respuestas</i></h2>

      <div class="table-responsive">
        <table class="table table-dark">
         <tr>
            <th>Numero de Pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr v-for="(respuesta, index) in respuestas" :key="index">
            <th>{{respuesta.pregunta}}</th>
            <th>{{respuesta.respuesta}}</th>

          </tr>
         
        </table>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-respuestas",
  props: [],
  mounted() {},
  data() {

    return {
     respuestas: [
       {pregunta: '1', respuesta: 'C'},
       {pregunta: '2', respuesta: 'C'},
       {pregunta: '3', respuesta: 'B'},
     ]
    };
  },
  methods: {},
  computed: {},
};
</script>

<style scoped lang="css">

.jumbotron {
  background-color: rgb(114, 114, 114);
  color: rgb(255, 255, 255);
}
</style>
