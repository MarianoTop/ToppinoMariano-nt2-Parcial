<template >

  <section class="src-componentes-formulario">
    <div class="jumbotron"> 
      <h1>Formulario</h1>

       <vue-form :state="formstate" @submit.prevent="enviar()">
        
        <!-- Campo nombre -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input type="text" id="nombre" v-model="formData.nombre" required 
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          name="nombre" autocomplete="off" class="form-control" />
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <!---Pareceria no tener sentido el mensaje dado que evita ingresar mayor cantidad-->
            <div slot="maxlength" class="alert alert-danger mt-1">
              Este campo no debe poseer más de {{ nombreMaxLength }} caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no admite espacios.
            </div>
          </field-messages>
          
        </validate>
        <br>

      
        <validate tag="div">
          <label for="descripcion">Descripcion</label>
          <input type="text" id="descripcion" v-model="formData.descripcion" required name="descripcion" autocomplete="off" class="form-control" />
    
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>
        <br>
        
        <!-- Campo deuda -->
        <validate tag="div">
          <label for="importe">Importe</label>
          <input type="number" id="importe" v-model.number="formData.importe" required name="importe" autocomplete="off" class="form-control" />
    
          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>

        <br>
        
       

        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>

      <!-- Tabla para representar los datos ingresados -->
      <h2>Detalle de Gastos</h2>
      <br>

      
      <div v-if="gastos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Descripcion</th>
            <th>Importe</th>
            <th>Fecha del gasto</th>           
          </tr>
          <tr v-for="(gasto,index) in gastos" :key="index" >
            <td>{{ gasto.nombre }}</td>
            <td>{{ gasto.descripcion }}</td>
            <td>${{ gasto.importe }}</td>            
            <td>{{ gasto.fecha }}</td>
           
          </tr>
          <tr :style="{color: analizarTotal().color}" >
            <td></td>
            <td></td>
            <td>Total</td>            
            <td>${{ total }}</td>
           
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-info">No hay gastos ingresados</h3>

    </div>
    
    



    
   
  </section>

</template>

<script >

  export default  {
    name: 'src-componentes-formulario',
     props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        gastos : [],
        nombreMinLength: 3,
        nombreMaxLength: 15,
        total:0,
      }
    },
    methods: {
      getInitialData() {
        return {
          gasto : null,
          descripcion: null,
          importe: null         
        }
      },
      enviar() {
        let gasto = {...this.formData}
        gasto.fecha = new Date().toLocaleString()

        console.log(gasto)
        this.gastos.push(gasto)
        this.total+=gasto.importe

        this.formData = this.getInitialData()
        this.formstate._reset()
      },      
      analizarTotal() {
        
        let color = 'green'
        if(this.total >= 1000) {
          color = 'magenta'
        }
          
        if(this.total > 5000) {
          color = 'orange'
        }
        return {
          color
        }
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron {
    background-color: lightslategray;
    color: white;
  }

  hr {
    background-color: black;
  }
</style>
