<template>
    <div>
      <table>
        <tbody>
            <h1>Id: {{fechasFaltantes.id}}</h1>
            <h1>fecha Inicio</h1>
            {{fechasFaltantes.fechaCreacion}}
            <h1>fecha Fin</h1>
            {{fechasFaltantes.fechaFin}}
            <h1>Fechas</h1>
            {{ fechasFaltantes.fechas}}
        </tbody>
      </table>
      <button v-on:click="checkRangeDate"> Agregar fechas </button>
    </div> 
    
</template>

<script>
import axios from 'axios';
import moment from 'moment';

export default {
    name:"fechasFaltantes",
    data(){
        return{
            fechasFaltantes: [],

        }
    },
    mounted() { 
      this.getFechasFaltantes();
      
    },
    methods: { 
      getFechasFaltantes() {
        axios.get('http://thor.advise.cl:8080/periodos/api')
        .then(response => {
          console.log(response);
          this.fechasFaltantes = response.data;
        })
        .catch(error => {
          console.log(error);
        });
      },
      checkRangeDate() {
        const formtearFecha = (fecha) => {
          return moment(fecha).format('YYYY-MM-DD');
        }
        if (this.fechasFaltantes.fechaCreacion && this.fechasFaltantes.fechaFin) {
          const fechaInicio = formtearFecha(this.fechasFaltantes.fechaCreacion);
          const fechaFin = formtearFecha(this.fechasFaltantes.fechaFin);
          const fechas = [];
          let fecha = fechaInicio;
          while (fecha <= fechaFin) {
            fechas.push(fecha);
            fecha = formtearFecha(moment(fecha).add(1, 'days'));
          }
          this.fechasFaltantes.fechas = fechas;
        }
      } 
      
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
