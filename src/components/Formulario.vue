<template>
  <section class="src-components-formulario">
     <div class="Formulario">
      <h2>Notas</h2>
        <hr>
        <br>
        <vue-form :state="formState" @submit.prevent="enviar()">
        
          <!-- --------------------- -->
          <!--     Campo nombre      -->
          <!-- --------------------- -->
          <validate tag="div">
            <label for="nombre">Nombre</label>
            <input 
              type="text"
              id="nombre"
              name="nombre" 
              class="form-control"
              autocomplete="off"
              v-model.trim="formData.nombre" 
              required 
              :minlength="nombreMinLength"
              :maxlength="nombreMaxLength"
              no-espacios
            />

            <field-messages name="nombre" show="$dirty">
              <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
              <div slot="minlength" class="alert alert-danger mt-1">
                Este campo requiere como mínimo {{nombreMinLength}} caracteres.
              </div>
              <div slot="maxlength" class="alert alert-danger mt-1">
                Este campo requiere como maximo {{nombreMaxLength}} caracteres.
              </div>
              <div slot="no-espacios" class="alert alert-danger mt-1">
                No se permiten espacios en este campo.
              </div>
            </field-messages>
          </validate>
          <br>

        <!-- --------------------- -->
        <!--    Campo apellido     -->
        <!-- --------------------- -->
        <validate tag="div">
          <label for="apellido">Apellido</label>
          <input 
            type="text"
            id="apellido"
            name="apellido" 
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.apellido" 
            required 
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          />

          <!-- Mensajes de validación -->
          <field-messages name="apellido" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
                Este campo requiere como mínimo {{nombreMinLength}} caracteres.
              </div>
              <div slot="maxlength" class="alert alert-danger mt-1">
                Este campo requiere como maximo {{nombreMaxLength}} caracteres.
              </div>
              <div slot="no-espacios" class="alert alert-danger mt-1">
                No se permiten espacios en este campo.
              </div>
          </field-messages>
        </validate>
        <br>

          <!-- ---------------------------- -->
          <!--             Nota             -->
          <!-- ---------------------------- -->
          <validate tag="div">
            <label for="nota">Nota</label>
            <input 
              type="number"
              id="nota"
              name="nota" 
              class="form-control"
              autocomplete="off"
              v-model.number="formData.nota" 
              required 
              :min="notaMin"
              :max="notaMax"
            />

            <field-messages name="nota" show="$dirty">
              <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
               <div slot="min" class="alert alert-danger mt-1">
                El minimo es {{notaMin}}.
              </div>
              <div slot="max" class="alert alert-danger mt-1">
                El maximo es {{notaMax}}.
              </div>
            </field-messages>
          </validate>
          <br>
          <br>

          <!-- Botón de envío -->
          <button class="btn btn-success my-4" :disabled="formState.$invalid">Enviar</button>
        </vue-form>   
         <hr>
        <span v-if="alumnos.length">
          <div class="table-responsive">
            <table class="table table-dark">
                <tr>
                    <th>Alumno</th>
                    <th>Nota</th>
                </tr>

                  <tr v-for="(alumno,index) in notasModificadas" :key="index" :class="alumno.colorNota">
                      <td>{{ alumno.nombre + ' ' + alumno.apellido}}</td>
                      <td>{{ alumno.nota}}</td>
                  </tr>
                  <tr>
                        <td>Promedio</td>
                        <td>{{calculoPromedio()}}</td>
                    </tr> 
            </table>
          </div>
        </span>

        <span v-else class="alert alert-warning">
                  No hay notas cargadas
        </span>
      <hr>
    </div>
  </section>
</template>

<script lang="js">
export default {
  name: 'src-components-formulario',
    props: [],
    mounted () {
    },
    data () {
      return {
        formState : {},
        formData : this.getInicialData(),
        nombreMinLength : 3,
        nombreMaxLength :15,
        notaMin: 0,
        notaMax: 10,
        alumnos: [],
        promedio: 0
      }
    },
    methods: {
      getInicialData() {
        return {
          nombre: '',
          apellido: '',
          nota: '', 
        }
      },
      enviar() {
         const alumno = {
          nombre: this.formData.nombre,
          apellido: this.formData.apellido,
          nota: this.formData.nota,
        }

        this.alumnos.push(alumno)
        this.formData = this.getInicialData()
        this.formState._reset()
      },

      calculoPromedio() {
        const sumaNotas=0;
        if(this.alumnos.length>0){
          let suma = this.alumnos.reduce((valorPrevio, alumno) => valorPrevio + alumno.nota, sumaNotas);
          this.promedio = suma / this.alumnos.length
        }
        return this.promedio
      }
    },
    computed: {
       notasModificadas: function () {
    return this.alumnos.map((alumno) => {
      let colorNota = null
      if(alumno.nota>=0 && alumno.nota<4){
        colorNota = "text-danger"  
      }else if(alumno.nota>=4 && alumno.nota<7){
        colorNota = "text-warning"
      }else{
        colorNota = "text-success"
      }
      return {
        nombre: alumno.nombre,
        apellido: alumno.apellido,
        nota: alumno.nota,
        colorNota: colorNota
      }
    })
    }
  }
}
</script>


<style scoped lang="css">

</style>
