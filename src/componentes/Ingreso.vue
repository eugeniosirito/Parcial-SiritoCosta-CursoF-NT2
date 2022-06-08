<template>
  <section class="src-componentes-ingreso">
    <div class="jumbotron">
      <h2><i>Ingreso de las Notas</i></h2>
      <hr />
      <br />

      <vue-form :state="formstate" @submit.prevent="enviar()">
        <!-- nombre -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input
            type="text"
            id="nombre"
            v-model="formData.nombre"
            required
            name="nombre"
            autocomplete="off"
            class="form-control"
            :minlength="cantidadMinLength"
            maxlength="15"
          />

          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Este campo es obligatorio
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como minimo
              {{ cantidadMinLength }} caracteres.
            </div>
          </field-messages>
        </validate>
        <br />

        <!-- apellido -->
        <validate tag="div">
          <label for="apellido">Apellido</label>
          <input
            type="text"
            id="apellido"
            v-model="formData.apellido"
            required
            name="apellido"
            autocomplete="off"
            class="form-control"
            :minlength="cantidadMinLength"
            maxlength="15"
          />

          <field-messages name="apellido" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Este campo es obligatorio
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como minimo
              {{ cantidadMinLength }} caracteres.
            </div>
          </field-messages>
        </validate>
        <br />

        <!-- nota -->
        <validate tag="div">
          <label for="nota">Nota</label>
          <input
            type="number"
            id="nota"
            v-model.number="formData.nota"
            required
            name="nota"
            autocomplete="off"
            class="form-control"
            :min="notaMin"
            :max="notaMax"
          />

          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Este campo es obligatorio
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              La nota minima puede ser {{ notaMin }}.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La nota minima puede ser {{ notaMax }}.
            </div>
          </field-messages>
        </validate>

        <br />

        <button
          class="btn btn-info my-3"
          :disabled="formstate.$invalid"
          type="submit"
        >
          Enviar
        </button>
      </vue-form>
      <br />
      <hr />

      <!-- historial de las notas -->
      <h2><i>Historial de notas</i></h2>
      <br />

      <div v-if="alumnos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Apellido</th>
            <th>Nota</th>
          </tr>
          <tr
            v-for="(nota, index) in alumnos"
            :key="index"
            :style="{ color: sacarPromedio(nota).color }"
          >
            <td>{{ nota.nombre }}</td>
            <td>{{ nota.apellido }}</td>
            <td>{{ nota.nota }}</td>
            <td>{{ sacarPromedio(nota).notaPintar }}</td>
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-danger">No hay alumnos ingresados</h3>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-ingreso",
  props: [],
  mounted() {},
  data() {
    return {
      formstate: {},
      formData: this.getInitialData(),
      alumnos: [],
      cantidadMinLength: 3,
      notaMin: 0,
      notaMax: 10,
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        apellido: null,
        nota: null,
        promedio: null,
      };
    },
    enviar() {
      let nota = { ...this.formData };
      console.log(nota);
      this.formstate._reset();
      this.alumnos.push(nota);
      this.formData = this.getInitialData();
    },

    /* prueba */
    sacarPromedio(nota) {
      let notaDeColor = nota.nota;
      let color = "#255";
      if (notaDeColor < 4) color = "#255";
      if (notaDeColor >= 4 && notaDeColor < 7) color = "#255";
      if (notaDeColor >= 4) color = "#255";
      return {
        notaPintada: notaDeColor,
        color,
      };
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: #6e6e6e;
  color: rgb(255, 255, 255);
  border: 5px inset rgba(12, 20, 133, 0.8);
}

hr {
  background-color: #999;
}

label {
  font-weight: bold;
}

pre {
  color: white;
}

td {
  color: white;
}
</style>
