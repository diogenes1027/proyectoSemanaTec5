<template>
    <v-container>
        <p>{{grafica}} en {{nombre}}</p>
            <v-progress-circular
      indeterminate
      color="primary"
      v-if="loading"
    ></v-progress-circular>

        <apexchart v-if="!loading" width="100%" type="line" :options="options" :series="series" v-bind:key="series[0].data"></apexchart>
    </v-container>
</template>

<script>
export default {
    props: ['pais','nombre','tipo','grafica'],

    watch:{
        series:function(newSeries,oldSeries){
            console.log(newSeries);
            console.log(oldSeries);
        },
        pais:function(){
            //console.log(newCripto)
            //console.log(oldCripto)
            this.cargarDatos();
        },
        grafica:function(){
            //console.log(newCripto)
            //console.log(oldCripto)
            this.cargarDatos();
        }
    },
    methods:{

        async cargarDatos(){
            this.loading=true;
            //TODO implementar aquí su llamada deberemos cambiar la data de categories y de data
            var datos=[]
            var fechas=[]
            await this.axios.get('https://api.covid19api.com/total/dayone/country/'+this.pais).then((response)=>{
                //console.log(response.data[0]);
                response.data.forEach(element => {
                    //console.log(element.Date)
                    fechas.push(element.Date)
                    if(this.tipo == 1){
                        datos.push(element.Confirmed)
                    }
                    else if (this.tipo == 2){
                        datos.push(element.Deaths)
                    }
                    else if (this.tipo == 3){
                        datos.push(element.Recovered)
                    }
                    else if (this.tipo == 4){
                        datos.push(element.Active)
                    }
                    
                });


            })
            this.options={
                xaxis:{
                    categories:fechas
                }
            }
            this.series = [{
                data: datos
            }]
            this.loading=false;
        }
    },

    data: ()=>({
        loading:false,
      options: {
        xaxis: {
        categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998],
        },
      },
      series: [{
        name: 'series-1',
        data: [30, 40, 45, 50, 49, 60, 70, 91]
      }]
    })
}
</script>