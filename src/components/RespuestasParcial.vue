<template>
  <section class="src-components-RespuestasParcial">
     <table class="table table-dark">
       <tr>
            <th>Numero de pregunta</th>
            <th>Respuesta</th>
        </tr>
       <tr v-for="(pregunta,index) in preguntas" :key="index">
            <td>{{pregunta.numero}}</td>
            <td>{{pregunta.respuestas}}</td>
      </tr>
        </table>
  </section>
</template>

<script lang="js">
export default {
  name: 'src-components-RespuestasParcial',
  props: [],
  mounted () {
  },
  data () {
    return {
      preguntas : [
        { numero: 1, respuestas: 'c' },
        { numero: 2, respuestas: 'c' },
        { numero: 2, respuestas: 'b' }
]
    }
  },
  methods: {
  },
  computed: {
  }
}
</script>


<style scoped lang="css">

</style>
