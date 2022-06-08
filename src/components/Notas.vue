<template lang="html">

  <section class="notas">
    <div class="jumbotron">
      <h2>Ingreso de Notas</h2>
      <vue-form :state="formState" @submit.prevent='send()'>
        <div class="wrapper my-3">
          <validate tag="div">
            <div class="field">
              <label for="name">Nombre</label>
              <input type="text" name="name" id="name" required v-model="formData.name" minlength="3" maxlength="15"
                @keydown.space="preventSpaces">
              <field-messages name="name" show="$dirty && $invalid">
                <div slot="required" class="alert alert-danger mt-1 ">
                  Este campo es requerido
                </div>
                <div slot="minlength" class="alert alert-danger mt-1 ">
                  No puede tener menos de 3 letras
                </div>
              </field-messages>
            </div>
          </validate>

          <validate tag="div">
            <div class="field">
              <label for="lastName">Apellido</label>
              <input type="text" name="lastName" id="lastName" required v-model="formData.lastName" minlength="3"
                maxlength="15">
              <field-messages name="lastName" show="$dirty && $invalid">
                <div slot="required" class="alert alert-danger mt-1 ">
                  Este campo es requerido
                </div>
                <div slot="minlength" class="alert alert-danger mt-1 ">
                  No puede tener menos de 3 letras
                </div>
              </field-messages>
            </div>
          </validate>

          <validate tag="div">
            <div class="field">
              <label for="grade">Nota</label>
              <input type="number" name="grade" id="grade" required v-model="formData.grade" min="1" max="10">
              <field-messages name="grade" show="$dirty && $invalid">
                <div slot="required" class="alert alert-danger mt-1 ">
                  Este campo es requerido
                </div>
                <div slot="min" class="alert alert-danger mt-1 ">
                  Se debe ingresar una nota mayor a 0
                </div>
                <div slot="max" class="alert alert-danger mt-1 ">
                  Se debe ingresar una nota menor o igual a 10
                </div>
              </field-messages>
            </div>
          </validate>

        </div>
        <button type="submit" :disabled="formState.$invalid"
          class="btn btn-success input-container mt-5">Submit</button>
      </vue-form>
    </div>

    <div class="tableWrapper jumbotron">
      <div v-if="!notas.length">
        <p> No hay notas ingresadas </p>
      </div>
      <table v-else class="table-secondary table">
        <thead>
          <tr>
            <th scope="col">Nombre</th>
            <th scope="col">Apellido</th>
            <th scope="col">Nota</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(nota, i) in notas" :key="i"
            :class="nota.grade < 4 ? 'table-danger' : nota.grade < 7 ? 'table-warning' : 'table-success'">
            <td>{{ nota.name }}</td>
            <td>{{ nota.lastName }}</td>
            <td>{{ nota.grade }}</td>
          </tr>
          <tr :class="getAverage() < 4 ? 'table-danger' : getAverage() < 7 ? 'table-warning' : 'table-success'">
            <td>Promedio</td>
            <td></td>
            <td>{{ getAverage() }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

</template>

<script lang="js">

export default {
  name: 'notas-component',
  props: [],
  mounted() {

  },
  data() {
    return {
      formState: {},
      formData: this.getInitialData(),
      notas: [],
    }
  },
  methods: {
    getInitialData() {
      return {
        name: null,
        lastName: null,
        grade: null,
      }
    },
    send() {
      this.notas.push(this.formData);
      this.getInitialData();
    },
    getAverage() {
      let avg = 0;
      let total = 0;
      this.notas.forEach(nota => {
        console.log(nota.grade), 'asd';
        total += +nota.grade;
        console.log(total)
      });
      avg = total / (this.notas.length);

      return avg;
    },
    preventSpaces(e) {
      if (!e.target.value) {
        e.preventDefault();
      } else if (e.target.value[0] == ' ') {
        e.target.value = e.target.value.replace(/^\s*/, "");
      }
    },
  },
  computed: {

  }
}


</script>

<style scoped lang="css">
.notas {}

input {
  width: 100%;
}

.jumbotron {
  margin-bottom: 0;
  background-color: #FCEBF6;
}

.tableWrapper {
  background-color: #ECE3FC;
  height: 100vh;
}

.wrapper {
  display: flex;
  justify-content: space-between;
}

.field {
  min-width: 25%;
}
</style>
