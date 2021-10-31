<template>
  <v-container>
    <h2>Encuesta sobre el regreso a clases</h2>
    
    
    <v-row>
            <v-col cols="3">
                <v-card style="padding:40px;">
                <v-text-field
                id="matricula"
                v-model="usuario.matricula"
                label="Matrícula"
                hide-details="auto"
                ></v-text-field>
                <v-text-field
                id="nombre"
                v-model="usuario.nombre"
                label="Nombre"
                hide-details="auto"
                ></v-text-field>
                <v-text-field
                id="edad"
                v-model="usuario.edad"
                label="Edad"
                hide-details="auto"
                ></v-text-field>
                <v-select
                    :items="nivele"
                    item-text="name"
                    v-model="usuario.nivel"
                    label="Nivel educativo"
                ></v-select>
                <v-switch
                v-model="usuario.regresa"
                :label="`regresarías a clases presenciales: `"
                ></v-switch>
            
                <v-btn id="botonAgregar"  style="margin-top:20px;" elevation="2" @click="agregarTodo" dark color="purple">Enviar</v-btn>      
                </v-card>
            </v-col>
            <v-col cols="9">
                <v-card style="padding:40px;">
                    <ReporteChart :contador=contador />
                </v-card>
            </v-col>
        </v-row>
   
  </v-container>
</template>

<script>
import ReporteChart from '../components/ReporteChart.vue'
  export default {
    components:{
        ReporteChart
    },

    name: 'Reporte',

    methods:{
      async agregarTodo(){
        await this.axios.post('https://backendst5.herokuapp.com/nuevo',this.usuario).then((response)=>{
            console.log(response);
        })
        this.contador=this.contador+1;
        
      },
      
      
    },
    data: () => ({
    
      contador:0,
      nivele:[
                {
                    id:1,
                    name:"Preparatoria"
                },
                {
                    id:2,
                    name:"Profesional"
                }
            ],
      usuario:{
        matricula:"",
        nombre:"",
        edad:"",
        nivel:"",
        regresa:false
      }
    }),
  }
</script>