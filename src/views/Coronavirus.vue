<template>
  <v-container>
      <h2>Coronavirus en el mundo</h2>
        <v-row style="margin-top:10px;">
            <v-col cols="12" md="6">
                <v-select
                :items="paises"
                item-text="Country"
                v-model="selectedCountry"
                label="Selecciona un país"
                return-object
                >
                </v-select>
            </v-col>
            <v-col cols="12" md="6">
                <v-select
                :items="tipodegrafica"
                item-text="name"
                v-model="selectedGraph"
                label="Datos de la gráfica"
                return-object
                >
                </v-select>
            </v-col>
            
                                 
        </v-row>

        <v-row>
            <v-col cols="3">
                <v-card style="padding:20px;">
                    <p><b>{{selectedCountry.Country}}</b></p>
                    <p>Casos totales: {{selectedCountry.TotalConfirmed}}</p>
                    <p>Muertes totales: {{selectedCountry.TotalDeaths}}</p>
                    <p>Nuevos casos: {{selectedCountry.NewConfirmed}}</p>
                    <p>Nuevas muertes: {{selectedCountry.NewDeaths}}</p>
                </v-card>
            </v-col>
            <v-col cols="9">
                <v-card style="padding:20px;">
                    <CoronaChart :pais="selectedCountry.Slug" :nombre="selectedCountry.Country" :tipo="selectedGraph.id" :grafica="selectedGraph.name"/>
                </v-card>
            </v-col>
        </v-row>
        

  </v-container>  
</template>

<script>
import CoronaChart from '../components/CoronaChart.vue'
    export default {
        components:{
            CoronaChart
        },
        name: 'Pais',
        async mounted(){
            
        await this.axios.get('https://api.covid19api.com/summary').then((response)=>{
            //console.log(response.data.Countries);
            this.paises = response.data.Countries;
        })
        },
        methods:{
            

        },
        data: () => ({
            paises:{},
            selectedCountry:[],
            selectedGraph:[],
            cargandoPaises:true,
            tipodegrafica:[
                {
                    id:1,
                    name:"Casos de coronavirus"
                },
                {
                    id:2,
                    name:"Muertes por coronavirus"
                },
                {
                    id:3,
                    name:"Casos de recuperación"
                },
                {
                    id:4,
                    name:"Casos activos de coronavirus"
                }
            ],
        }),
    }
  
</script>
